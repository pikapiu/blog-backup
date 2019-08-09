---
title: 深入浅出volatile
date: 
categories: java
tags: 
 - java
 - volatile
thumbnail: /images/wolf.jpg
---

## 深入浅出volatile
- __用途：__ 
    - 保证变量可见性
    - 限制局部代码指令重排序

    ![](/images/v.png)

#### volatile语义规范：
- 使用volatile变量时，必须重新从主内存中加载，并且read、load是连续的
- 修改volatile变量后，必须立刻同步到主内存，并且store、write是连续的
---
#### volatile不是线程安全的
- __原因：__ 因为没有锁机制，线程可以并发操作同一资源
---
### volatile的使用场景

#### 使用范围
    1.volatile只可修饰成员变量（静态的和非静态的都可以），因为局部变量是线程独享的
    (java中没有全局变量这个概念，那个是c的，静态成员变量是属于类的，非静态则是对象的)

    2.多线程并发下，才需要使用它
#### 使用场景
 - 只有一个修改者，多个使用者，要求保证可见性的场景

     1.状态标识

     2.数据定期发布，多个获取者

