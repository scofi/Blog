### Redis bitmap 占用内存大问题

#### Bitmap的数据结构
  Bitmap 的底层数据结构用的是 String 类型的 SDS 数据结构来保存位数组，Redis 把每个字节数组的 8 个 bit 位利用起来，每个 bit 位 表示一个元素的二值状态（不是 0 就是 1）。

可以将 Bitmap 看成是一个 bit 为单位的数组，数组的每个单元只能存储 0 或者 1，数组的下标在 Bitmap 中叫做 offset 偏移量。

为了直观展示，我们可以理解成 buf 数组的每个字节用一行表示，每一行有 8 个 bit 位，8 个格子分别表示这个字节中的 8 个 bit 位，如下图所示：
![avatar](https://segmentfault.com/img/remote/1460000040177144)

#### Bitmap 命令
* SETBIT 命令
```
SETBIT <key[string]> <offset[int]> <value[0,1]>
```
* GETBIT 命令
```
GETBIT <key[string]> <offset[int]>
```
* BITCOUNT 命令
```
BITCOUNT <key[string]>
```
* BITPOS 命令
```
 BITPOS key bitValue [start] [end]
```

### 问题
当知晓setbit命令时，如果offset的值很大，那么bitmap占用的字节数就越多，下面是测试情况：
* 首先测试offset值比较小的情况
    ```
    127.0.0.1:6379[1]> setbit t1 1 1
    (integer) 0
    127.0.0.1:6379[1]> memory usage t1
    (integer) 56  (单位是字节)
    ```
    由上面结果可以看到占用内存很小，下面我们加大offset

* 测试offset值为1000
    ```
    127.0.0.1:6379> setbit t2 1000 1
    (integer) 0
    127.0.0.1:6379> memory usage t2
    (integer) 208
    127.0.0.1:6379>
    ```
可以看到占用内存比上面大了很多，下面再来测试1000000
* 测试offset值为1000000
127.0.0.1:6379> setbit t3 1000000 1
(integer) 0
127.0.0.1:6379> memory usage t3
(integer) 131120
根据上面可以看到 offset越大，占用的内存就越大，redis会把从1一直到offset所有的数字都算上了（值默认是0）。

当我们使用bitmap时如果offset很大，有时候会用用户ID作为offset，如果我们的用户很多用户ID很大，比如是：100000000，此时这个key占用的内存是12M左右，这样的key越来越多时候，就会容易大量消耗内存，所以在使用时候要注意。

### 措施
* bitmap key不能太多，offset尽量从小开始，这样占用内存最少。
* 如果key比较多，就要注意offset 最大值情况，要避免占用大内存。