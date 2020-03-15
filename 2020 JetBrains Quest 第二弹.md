# 2020 JetBrains Quest 第二弹

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200312102225.png?x-oss-process=style/small)

## 开始

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200312085145.png?x-oss-process=style/small)

在第一弹提交之后，收到的邮件的末尾，写了第二弹游戏开始的时间：

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200312085324.png?x-oss-process=style/small)



![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200312085405.png?x-oss-process=style/small)

果然准时发布了，let's go !

参考了[这个帖子](https://v2ex.com/t/651961)以及以下的一些回复，以及[这个Gist](https://gist.github.com/lisachensyd/122e815c972129cda841e39d4ccbb217)，感谢大佬们分享的思路。

## 过程

```java
Time for the next #JetBrainsQuest!
.spleh A+lrtC/dmC .thgis fo tuo si ti semitemos ,etihw si txet nehw sa drah kooL .tseretni wohs dluohs uoy ecalp a si ,dessecorp si xat hctuD erehw esac ehT .sedih tseuq fo txen eht erehw si ,deificeps era segaugnal cificeps-niamod tcudorp ehT
```

这一串文字，一看熟悉的```A + lrtC```,经常 Ctrl +A ,Shift +Delete的同学可能就看出来了，这段文字是经过reverse的，用Java ~~一行~~ 代码就可以搞定![tieba_emotion_88](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/tieba_emotion_88_1571074484712.png?x-oss-process=style/small)

```java
text = new StringBuffer(text).reverse().toString();
```

于是得到了：

```The product domain-specific languages are specified, is where the next of quest hides. The case where Dutch tax is processed, is a place you should show interest. Look hard as when text is white, sometimes it is out of sight. Cmd/Ctrl+A helps.```

如果你直接copy第一句话来google一下的话，大概率会和我一样，来到这个页面：

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200312091113.png?x-oss-process=style/small)

不过这是不对的，我在这个页面逛了好一会。。啥玩意也没有找到，其实应该去的是MPS的[产品页](https://www.jetbrains.com/mps/)

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200312091348.png?x-oss-process=style/small)

直接搜索 Dech tex 定位到的地方，点进去会看到一个PDF:

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200312091538.png?x-oss-process=style/small)

乍一看平平无奇，但是还记得推文说的那句吗```sometimes it is out of sight. Cmd/Ctrl+A helps```

好的那就Ctrl + A全部选中试一下，有些网站 ~~好孩子看不见~~ 。

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200312091809.png?x-oss-process=style/small)

这块地方有点不对劲，让我们复制到别的地方粘贴一下康康：

```This is our 20th year as a company, we have shared numbers in our JetBrains Annual report, sharing the section with 18,650 numbers will progress your quest.``

ok ，进度条向前走了一丢丢，距离成功还有一大步！

这句话的提到了**JetBrains Annual report**,看看去

找到了距今最新发布的[JetBrains 2019 Annual](https://www.jetbrains.com/company/annualreport/2019/), 不过提到的18650是啥意思？

直接搜索18650：

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200312092353.png?x-oss-process=style/small)

结果是0

这咋整，删掉几个数字试试，扩大范围。搜18试试(这一步是我知道了答案才想到的，一开始没有想到)

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200312092605.png?x-oss-process=style/small)



其实这些数字加起来，正好是18650，看到那个转发按钮了吗，点它！

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200312092731.png?x-oss-process=style/small)

竟然藏在分享的编辑栏里，这波可以啊，复制出来看看说的啥：

```I have found the JetBrains Quest! Sometimes you just need to look closely at the Haskell language, Hello,World! in the hackathon lego brainstorms project https://blog.jetbrains.com/blog/2019/11/22/jetbrains-7th-annual-hackathon/ #JetBrainsQuest```

给了个博客链接，点进去，直接搜索**brainstorms**

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200312094849.png?x-oss-process=style/small)

有一幅图，莫非这图里有什么玄机，翻来覆去看了好几遍。。一无所获，遂看提示，原来藏在图片的alt里

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200312095051.png?x-oss-process=style/small)



```d1D j00 kN0w J378r41n2 12 4lW4Y2 H1R1N9? ch3CK 0u7 73h K4r33r2 P493 4nD 533 1f 7H3r3 12 4 J08 F0r J00 0R 4 KW357 cH4LL3n93 70 90 fUr7h3r @ l3457.```

这玩意又给我卡住了，觉得像是什么加密的字符，搜索了一圈也搜索不到，一眼看上去压根毫无规律可言嘛。

继续看了[gist](https://gist.github.com/lisachensyd/122e815c972129cda841e39d4ccbb217)提示，才知道这是嘤文的火星文，≮о我，厵莱昰這樣孓≯ 。

翻译过来就是

```Did you know Jetbrains is always hiring? Check out the kareers(careers) page and see if there is a job for you or for kwest(quest) challenge to go further at least.```

我："你是怎么认识火星文的"

大佬："就...脑补啊"

666666

在大佬的提示下，我才知道原来获得邀请码的邮件里也藏着个彩蛋：

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200312095848.png?x-oss-process=style/small)

Y0U H4V3 R3C13V3D 7H15 3M41L B3C4U53 Y0U H4V3 P4RT1C1P4T3D 1N J3TBR41N5 QU35T

You have recieved this email because you have participate in jetbrains quest

动手翻译了一下，还是hin有意思的，而且得到了一个字典，先给自己挖个坑。

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200312100048.png?x-oss-process=style/small)

扯远了，继续解题。

Jetbrains is always hiring? 

去[职位发布页面](https://www.jetbrains.com/careers/jobs/)看看, 注意一下**careers**这个词，就不会迷了路

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200312100514.png?x-oss-process=style/small)



在页面上搜索quest：
![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200312100725.png?x-oss-process=style/small)

点进去看看：

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200312100811.png?x-oss-process=style/small)

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200312100922.png?x-oss-process=style/small)

i'm felling lucky !

看一下啥是cheat at Konami games:

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200312101040.png?x-oss-process=style/small)

上上下下左右左右BA，原来它还有个专业的名字，叫做Konami Code !

魂斗罗30条命！我来辽！！

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200311214007.png?x-oss-process=style/small)

上上下下左右左右BA



<img src="https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200311211705.png?x-oss-process=style/small"  />



wow, awesome!

这是我独享的moment![tieba_emotion_93](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/tieba_emotion_93_1571074484841.png?x-oss-process=style/small)