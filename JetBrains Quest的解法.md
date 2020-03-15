# JetBrains Quest的解法

## 来由

昨天在V站看到个[帖子](https://jp.v2ex.com/t/651662),题为「JetBrains Quest，解开可获得全家桶三个月免费订阅」，当时没太在意，今天又看到了，突然来了兴致，遂试了一试，参考了帖子底下的一些回复以及这篇[文章](https://mihajlonesic.gitlab.io/archive/jetbrains-quest/)。

[文章](https://mihajlonesic.gitlab.io/archive/jetbrains-quest/)的作者由于帖子访问量过高，怕直接全部给出答案会让活动失去了乐趣，于是隐去了一段，不过给了个小tip, 着实让我思考了一会儿，最后灵光一闪，解了出来。

> ### Due to high traffic on this page, I’ve decided to remove the rest of the blog post since I don’t know if JetBrains is ok with this. Also I don’t want to spoil the fun! I will bring back the solution once the quest is over.



## 过程

JetBrains官方发了一条[推](https://twitter.com/jetbrains/status/1236986174075482113)：

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200311114949.png?x-oss-process=style/small)

```lua
48 61 76 65 20 79 6f 75 20 73 65 65 6e 20 74 68 65 20 73 6f 75 72 63 65 20 63 6f 64 65 20 6f 66 20 74 68 65 20 4a 65 74 42 72 61 69 6e 73 20 77 65 62 73 69 74 65 3f
```

这个玩意打眼一瞧，很像是16进制，直接google了一下，

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200311115345.png?x-oss-process=style/small)

得到了text:

>Have you seen the source code of the JetBrains website?

接下来打开 [JetBrains的官网](https://www.jetbrains.com/)，Ctrl + U 或者鼠标右键， 打开查看页面源代码，

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200311115749.png?x-oss-process=style/small)

Ctrl + F 搜索 Quest，看到了说明，意思是让去官方的产品页面，找一个Joke,同时给了一个线索：```Good luck! == Jrrg#oxfn$```, 看不出来这是干嘛的，暂且记下，待会儿应该会有用。

接下来按照指示，去往[产品页面](https://www.jetbrains.com/products.html), 说明文字提示这个页面需要在chrome的无痕模式下打开，其实这是个Joke,普通模式也可以，打开之后你将看到这样一个页面：

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200311131132.png?x-oss-process=style/small)

找到了，就是这个JK!

点击learn more,弹出了一个页面：

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200311144102.png?x-oss-process=style/small)

给了个短网址：https://jb.gg/###

###是省略了的参数，答案是500 到 5000之中一共有多少个质数，哈哈哈我也很喜欢质数。

然后继续google一下，找到了[一个网站](https://miniwebtool.com/list-of-prime-numbers/?to=5000)，可以列出1到10000以内的质数

接下来就好办了，一个简单的减法得到答案是574

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200311132021.png?x-oss-process=style/small)

​	拼到刚才获得到的那个短网址上：https://jb.gg/574

打开之后来到了PyCharm的说明书，里面藏了个彩蛋：

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200311132550.png?x-oss-process=style/small)

台球桌上的那张卡片写着 MPS-31816,还画着一个logo,那个logo看起来也是JetBrains的一个产品，直接搜一下看看：

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200311132925.png?x-oss-process=style/small)



点进去康康：

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200311133007.png?x-oss-process=style/small)

看到这样一句话：

> “The key is to think back to the beginning.” – The JetBrains Quest team

beginning? 等等，一开始我们是不是有个线索还没用到来着，就是这个:```Good luck! == Jrrg#oxfn$```

然后又一串挺长的鬼画符：

```Qlfh$#Li#|rx#duh#uhdglqj#wklv#|rx#pxvw#kdyh#zrunhg#rxw#krz#wr#ghfu|sw#lw1#Wklv#lv#rxu#lvvxh#wudfnhu#ghvljqhg#iru#djloh#whdpv1#Lw#lv#iuhh#iru#xs#wr#6#xvhuv#lq#Forxg#dqg#iru#43#xvhuv#lq#Vwdqgdorqh/#vr#li#|rx#zdqw#wr#jlyh#lw#d#jr#lq#|rxu#whdp#wkhq#zh#wrwdoo|#uhfrpphqg#lw1#|rx#kdyh#ilqlvkhg#wkh#iluvw#Txhvw/#qrz#lw“v#wlph#wr#uhghhp#|rxu#iluvw#sul}h1#Wkh#frgh#iru#wkh#iluvw#txhvw#lv#‟WkhGulyhWrGhyhors†1#Jr#wr#wkh#Txhvw#Sdjh#dqg#xvh#wkh#frgh#wr#fodlp#|rxu#sul}h1#kwwsv=22zzz1mhweudlqv1frp2surpr2txhvw2```

我看到这篇[文章](https://mihajlonesic.gitlab.io/archive/jetbrains-quest/)说提示是**Caesar cipher**

[V站的帖子](https://jp.v2ex.com/t/651662)里38楼给了个[这个网站](https://www.dcode.fr/caesar-cipher)

打开看看：

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200311133816.png?x-oss-process=style/small)

一股洪荒的气息涌来，直接把上面那串“乱码”copy过来试试：

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200311134004.png?x-oss-process=style/small)

看到最后一行的时候，我脑子里自动把```2```替换成了```/```，这很明显是个网址嘛！

于是手动解码成 https://www.jetbrains.com/promo/quest/

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200311134300.png?x-oss-process=style/small)

哈哈哈，我成功了！这个Code很显然就是那个什么Good Luck后面的 ```Jrrg#oxfn$```这一串嘛！

于是：

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200311134521.png?x-oss-process=style/small)

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200311134544.png?x-oss-process=style/small)

竟然是Wrong answer！这我就很懵了。。

我觉得我好像是漏了点什么，于是又回到那个解凯撒密码的网站仔细琢磨了一下

刚才解码得到好长一串，我只是猜了最后的网址，还有很多没有用到，里面会不会隐藏一些线索呢？

于是我又仔细看了一遍：

\```Nice$#If#|ou#are#reading#this#|ou#must#have#worked#out#how#to#decr|pt#it1#This#is#our#issue#tracker#designed#for#agile#teams1#It#is#free#for#up#to#6#users#in#Cloud#and#for#43#users#in#Standalone/#so#if#|ou#want#to#give#it#a#go#in#|our#team#then#we#totall|#recommend#it1#|ou#have#finished#the#first#Quest/#now#it“s#time#to#redeem#|our#first#pri}e1#The#code#for#the#first#quest#is#‟TheDriveToDevelop†1#Go#to#the#Quest#Page#and#use#the#code#to#claim#|our#pri}e1#https=22www1jetbrains1com2promo2quest2```

这些```#```太碍眼了，得想办法去掉，我又想起了那串密文，```Jrrg#oxfn$```

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200311140912.png?x-oss-process=style/small)

解出来 Good#luck$, 但是原文是Good luck!, 说明加密规则肯定不是这个Shift by 3

所以问题就变成了寻找这个加密规则。

然后我又在DECRYPT CAESAR CODE 这个按钮底下看到了 ROT Ciper

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200311142236.png?x-oss-process=style/small)

规则原来是 ASCII+3，把刚才那个密文解了看看，啊，顿时感觉英语单词是如此的顺眼！

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200311142543.png?x-oss-process=style/small)

但是这个网站有解密的字符长度限制，显示的解密结果不全，想来是为了节省算力吧，没关系，记下前半句，接下来把密文随便从中间去掉一半，后半段再次解密

过程我就不放图了，重复了几下，凑出了一小段语义完整的话，中间的重点是这句：

>  The code for the first quest is TheDriveToDevelop.

找到就是你！ TheDriveToDevelop

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200311143133.png?x-oss-process=style/small)

很愉快的提交啦，然而不幸的是，我并么有收到jetBrains发来的邮件。。我也不知道为啥，不过过程还是挺有意思的。

