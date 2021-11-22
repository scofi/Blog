### 安装和配置
#### 重要概念
* JDK
> JDK(Java SE Development Kit)，Java标准开发包，它提供了编译、运行Java程序所需的各种工具和资源，包括Java编译器、Java运行时环境，以及常用的Java类库等。
* JRE
> JRE( Java Runtime Environment) 、Java运行环境，用于解释执行Java的字节码文件。普通用户而只需要安装 JRE（Java Runtime Environment）来运行 Java 程序。而程序开发者必须安装JDK来编译、调试程序。
* JVM  
> JVM(Java Virtual Mechinal)，Java虚拟机，是JRE的一部分。它是整个java实现跨平台的最核心的部分，负责解释执行字节码文件，是可运行java字节码文件的虚拟计算机。所有平台的上的JVM向编译器提供相同的接口，而编译器只需要面向虚拟机，生成虚拟机能识别的代码，然后由虚拟机来解释执行。

#### 安装和配置
* 下载
> https://www.oracle.com/java/technologies/downloads/
* 安装
> 双击安装
* 配置

编辑.bash_profile
>export JAVA_16_HOME=/Library/Java/JavaVirtualMachines/jdk-16.0.2.jdk/Contents/Home  
export JAVA_8_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_311.jdk/Contents/Home  
export JAVA_HOME=$JAVA_8_HOME  
export PATH=$JAVA_HOME:$PATH  
source ~/.bashrc

之后执行
> source .bash_profile