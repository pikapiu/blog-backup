---
title: java面试题（未完待续）
date: 
categories: java
tags: 
 - java
 - interview
thumbnail: /images/girl.jpg
---

### hashmap的基本原理，内部数据结构，put操作的整体流程，是否线程安全以及为什么?jdk8对hashmap做了哪些优化？
- __HashMap 性能O(1),TreeMap O(log n)__ 

- HashMap基于哈希思想，实现对数据的读写。当我们将键值对传递给put()方法时，它调用键对象的hashCode()方法来计算hashcode，然后找到bucket位置来储存值对象。
当获取对象时，通过键对象的equals()方法找到正确的键值对，然后返回值对象。

- HashMap使用链表来解决碰撞问题，当发生碰撞了，对象将会储存在链表的下一个节点中。

- HashMap在每个链表节点中储存键值对对象。当两个不同的键对象的hashcode相同时，它们会储存在同一个bucket位置的链表中，可通过键对象的equals()方法用来找到键值对。
如果链表大小超过阈值（TREEIFY_THRESHOLD, 8），链表就会被改造为树形结构。

- HashMap默认容量为16，且要求容量一定为2的整数次幂。

- HashMap不支持线程的同步，即任一时刻可以有多个线程同时写HashMap;可能会导致数据的不一致。

- __TreeMap(基于红黑树):所以一般需要排序的情况下是选择TreeMap来进行，默认为升序排序方式（深度优先搜索），可自定义实现Comparator接口实现排序方式。__

- __HashMap并不是线程安全的__
    1.可以用 Collections的synchronizedMap方法；
    2.使用ConcurrentHashMap类。

        相较于HashTable锁住的是对象整体，ConcurrentHashMap基于lock实现锁分段技术。
        首先将Map存放的数据分成一段一段的存储方式，然后给每一段数据分配一把锁，当一个线程占用锁访问其中一个段的数据时，
        其他段的数据也能被其他线程访问。
        ConcurrentHashMap不仅保证了多线程运行环境下的数据访问安全性，而且性能上有长足的提升。
---

### String类为什么是不可变的？StringBuilder和StringBuffer的区别，字符串常量池，StringBuffer为什么是线程安全？加号的底层原理

- 只有当字符串是不可变的，字符串池才有可能实现。字符串池的实现可以在运行时节约很多heap空间，因为不同的字符串变量都指向池中的同一个字 符串。但如果字符串是可变的，
那么String interning将不能实现(译者注：String interning是指对不同的字符串仅仅只保存一个，即不会保存多个相同的字符串。)，因为这样的话，如果变量改变了它的值，那么
其它指向这个值的变量 的值也会一起改变。

- 如果字符串是可变的，那么会引起很严重的安全问题。譬如，数据库的用户名、密码都是以字符串的形式传入来获得数据库的连 接，或者在socket编程中，主机名和端口都是以字
符串的形式传入。

- 因为字符串是不可变的，所以是多线程安全的，同一个字符串实例可以被多个线程共享。这样便不用因为线程安全问题而使用同步。字符串自己便是线程安全的。

- 类加载器要用到字符串，不可变性提供了安全性，以便正确的类被加载。

- .因为字符串是不可变的，所以在它创建的时候hashcode就被缓存了，不需要重新计算。这就使得字符串很适合作为Map中的键，字符串的处理速度要快过其它的键对象。这就是HashMap
中的键往往都使用字符串。

__String对“+”的重载__

```
public static void main(String[] args) {
    String string="hello";
    String string2 = string + "world";
```

***反编译之后***

```
public static void main(String args[]){
   String string = "hello";
   String string2 = (new StringBuilder(String.valueOf(string))).append("world").toString();
}
```

看了反编译之后的代码我们发现，其实String对“+”的支持其实就是使用了StringBuilder以及他的append、toString两个方法。

__String.valueOf(int  i) 也是调用 Integer.toString(i) 实现的__

```
public static String valueOf(int i) {
    return Integer.toString(i);
}
```

---
##### 未完待续

