## Java中的Integer缓存



太长不看版![tieba_emotion_92](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/tieba_emotion_92_1571074484843.png?x-oss-process=style/small) ：

> Java中比较包装类型的变量值时，要使用.equals()方法。除非那几个值是在缓存范围之内的，可以直接用双等于。

Java中的**Integer**/ˈɪntɪdʒər /，和**String**，可以说是非常常见了，今天来看一看Integer的一部分源码。**String**留着下次写。

先从几行比较数值的代码讲起：

```java
        Integer a = 99;
        Integer b = 99;
        Integer c = 180;
        Integer d = 180;
        System.out.println(a == b);
        System.out.println(c == d);
```

这个打印出来的两个结果分别是 ```true;false```

a，b，c，d 分别是4个Integer类型的对象，而 == 比较的是两个对象的地址是否相同，所以上述结果的意思是a和b竟然指向同一个对象？？而c和d是不同的两个对象？

同样是Integer ,为何会有不一样的结果呢？

Java的几个包装类都有自己的.valueOf()方法来初始化变量，让我们点进Integer，看一看它的valueOf()

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200324204729.png?x-oss-process=style/small)

IntegerCache.low? high?

看来问题出在这玩意上了，点进去可以看到：

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200324204959.png?x-oss-process=style/small)



原来如此，Java中Integer类型变量的值，如果在-128和127之间，就会从一个已经缓存好了的数组中直接取。

而且这个high可以通过 ```-Djava.lang.Integer.IntegerCache.high = X```进行更改：

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200324205426.png?x-oss-process=style/small)

然后再次运行，我就得到了两个true。

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200324205500.png?x-oss-process=style/small)

也可以通过虚拟机参数 ``` -XX:AutoBoxCacheMax = X``` 来修改这个high 。

为什么缓存这个呢，因为相较于其他的数值，这些数值太常用了，经常 status == 0?吧，经常int i =  0 吧？





