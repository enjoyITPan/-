## 一、volatile

### 1.1、定义

> 当多线程访问共享变量时，如果一个变量被声明为volatile时，java的**内存模型**可以保证所有的线程看到的这个变量值是一致的。

### 1.2、实现原理

​		volatile底层是借助了cpu的指令实现的。当编译器讲java 代码编译成汇编指令时，会检查变量是否被volatile修饰，如果被修饰了，在转化为汇编代码时，会增加一个**lock**指令。

​		lock指令会引发两件事：

​			1、将当前处理器缓存行的值写回缓存；（cpu执行操作时，会将数据先读入内部缓存（L1,L2等））

​			2、同时使其他cpu的缓存数据失效；（每个处理器通过嗅探在数据总线上传播的数据检查当前自己的缓存数据是否有效）



## 二、synchronize

### 2.1、定义

​	java中的每个对象都可以是锁。表现为如下情况：

​		1、对于普通方法，锁的是当前实例；

​		2、对于静态方法，锁的是当前类的Class对象；

​		3、对于同步方法块，锁的是Synchronize括号里配的对象。

### 2.2、 优化

1、偏向锁

​		大多数程序中，锁不仅不存在竞争，而且总是由同一个线程获得。为了减少线程获取锁的代价，引入了偏向锁。

对象头：存储锁偏向的线程Id；

cas进行加锁和解锁：只需要判断对象头有没有当前线程的id，没有就利用cas尝试竞争锁。

2、轻量锁

​      线程执行同步代码块之前，先在当前线程的栈帧中创建存储锁记录的空间，并将对象头中的Mark word复制到栈中，然后尝试使用cas替换指向记录的指针，成功则获取锁，否则使用自旋来获取锁。



## 三、ReentrantLock & AQS





​	

