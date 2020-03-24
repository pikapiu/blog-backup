---
title: Java中的Error和Exception
date: 
categories: java
tags: 
 - java
 - error
 - exception
thumbnail: /images/winter.jpg
---
![](/images/error_exception.png)
- __平时代码中接触到的多是Exception，Error更多在JVM内部出现，比如OutofMemory,stackOverFlow__

### Exception

1. 如参数是个非空集合却传入了空值（为什么此时用异常合适，因为需要在出现时给调用方些强提示，带些信息上去）

```
public void method(String[] args) {
        int temperature = 0;
        if (args.length > 0) {
            try {
                temperature = Integer.parseInt(args[0]);
            }
            catch(NumberFormatException e) {
                throw new IllegalArgumentException(
                    "Must enter integer as first argument, args[0]="+args[0],e);
            }
        }
}
```

2. （Method）知道有问题，但自己处理不了,比如读取文件。

#### checkedException 

> Java 要求必须在函数头部写上“throws XXXException”，否则它就编译不通过。这个声明表示函数在某些情况下，会抛出 XXXException 这个异常。由于编译器看到了这个声明，它会严格检查你对该函数的用法。在调用该函数的时候，你必须使用 try-catch 处理这个异常，或者在调用的函数头部也声明 “throws XXXException”，把这个异常传递给上一层调用者。

#### checkedException 和 RuntimeException的选择

首先从调用方开始考虑，如果是调用方破坏了协议，则抛出运行时异常，这类异常一般出现可能性较低，调用方已知，所以没必要强制调用方抓此异常。

然后如果问题出现在被调用方，无法正常执行完成工作，这时候考虑该问题调用方是否可以处理。
如果能处理，比如文件找不到、网络超时，则抛检查时异常否则比如磁盘满，抛运行时异常。

> 1. 抓异常宜晚，抛异常宜早。
> 2. 不要抓了，又把异常吞掉，不留下一丝痕迹
> 3. 不要抓住异常，打行日志完事儿。
> 4. 不要将异常状态流和业务状态流混在一起。

### NoClassDefFoundError 和 ClassNOtFoundException

> NoClassDefFoundError是一个错误(Error)，而ClassNOtFoundException是一个异常，在Java中对于错误和异常的处理是不同的，我们可以从异常中恢复程序但却不应该尝试从错误中恢复程序。

#### ClassNotFoundException的产生原因：

- Java支持使用Class.forName方法来动态地加载类，任意一个类的类名如果被作为参数传递给这个方法都将导致该类被加载到JVM内存中，如果这个类在类路径中没有被找到，那么此时就会在运行时抛出ClassNotFoundException异常。

##### 解决方法：
确保所需的类连同它依赖的包存在于类路径中，常见问题在于类名书写错误。
另外还有一个导致ClassNotFoundException的原因就是：当一个类已经某个类加载器加载到内存中了，此时另一个类加载器又尝试着动态地从同一个包中加载这个类。通过控制动态类加载过程，可以避免上述情况发生。

#### NoClassDefFoundError：

- 如果JVM或者ClassLoader实例尝试加载（可以通过正常的方法调用，也可能是使用new来创建新的对象）类的时候却找不到类的定义。要查找的类在编译的时候是存在的，运行的时候却找不到了。这个时候就会导致NoClassDefFoundError

- 造成该问题的原因可能是打包过程漏掉了部分类，或者jar包出现损坏或者篡改。解决这个问题的办法是查找那些在开发期间存在于类路径下但在运行期间却不在类路径下的类。




















