## 面向对象
### 继承
* 向上转型
> 一个引用类型为父类的变量，指向子类类型的实例
```
// Person为父类，Students为子类
// 类型安全
Person p = new Students();
```
* 向下转型
> 一个引用类型为子类的变量，指向父类类型的实例
```
// 不安全，子类可能有新方法
Students s = new Person();
```
### 继承和组合
* 继承是is a关系，子类是父类的一种，例如：燕子是鸟的一种，燕子是鸟的子类，是继承关系。
* 组合是has a关系，B类是A类的一部分，两个对象之间是整体和部分的关系，例如：轮子是汽车的一部分，即组合关系

### 多态
* 引用类型指向的具体对象，必须在由程序运行期间才能决定
```
多态就是指程序中定义的引用变量所指向的具体类型和通过该引用变量发出的方法调用在编程时并不确定，而是在程序运行期间才确定，即一个引用变量倒底会指向哪个类的实例对象，该引用变量发出的方法调用到底是哪个类中实现的方法，必须在由程序运行期间才能决定。因为在程序运行时才确定具体的类，这样，不用修改源程序代码，就可以让引用变量绑定到各种不同的类实现上，从而导致该引用调用的具体方法随之改变，即不修改程序代码就可以改变程序运行时所绑定的具体代码，让程序可以选择多个运行状态，这就是多态性。
```