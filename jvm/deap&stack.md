# 堆和栈的区别

## 功能不同

* 栈内存用来存储局部变量和方法调用。
* 而堆内存用来存储Java中的对象。无论是成员变量，局部变量，还是类变量，它们指向的对象都存储在堆内存中。

## 共享性不同
* 内存是线程私有的。
* 堆内存是所有线程共有的。

## 异常错误不同

如果栈内存或者堆内存不足都会抛出异常。

栈空间不足：java.lang.StackOverFlowError。
堆空间不足：java.lang.OutOfMemoryError。

## 空间大小

栈的空间大小远远小于堆的。
