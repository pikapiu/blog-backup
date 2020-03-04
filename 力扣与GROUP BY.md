

力扣与GROUP BY

## 写在前面

不说别人，只说我自己，从第一次知道leetcode距今已有三年了。。然而一直停留在两数之和。

当我遇到一个未知的事情，第一反应是：我怎么这么晚才知道！我应该早点知道的。

我永远嫌弃自己知道的太晚。这是病，得治。

任何事情，当你知道的那一刻，那就是最早的时候。

说来也挺可笑的，我当初还嫌弃[力扣](https://leetcode-cn.com/)是中文版的，逼格不够高，心里想着，等我过两天，就从 [leetcode](https://leetcode.com/)刷起，然而这么久了，没有一个平台能坚持超过3道题的，后来知道了 [TC](https://www.topcoder.com/)和 [CF]( www.codeforces.com)，走马观花的逛了一下之后，给我整自闭了——这些都是人能解出来的题目吗？

虽然我早就知道自己不是什么天才，就一普通人。但是真的好不甘心啊。

好了，不比比了，话锋一转，说说 **GROUP BY**

## GROUP BY

我一度不知道，GROUP BY 的列和SELECT后面的列之间的关系到底是怎样的，今天终于搞明白个123，特此记录下来。

由于我懒得再跑去服务器装个数据库了，就随便找了个 [在线练习SQL的网站](https://sqlzoo.net/wiki/SELECT_basics/zh)

界面简~~陋~~洁优雅，拥有一个表，名叫world，首先，按照惯例：

![sqlzoo](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200304171459.png?x-oss-process=style/small)

:laughing:

不过我随后又发现，这个表的name没有重复的。。所以不适合当作本次的示例，果断跑路，还是借用题目所给的那张表吧，直接写云SQL就完事了，题目如下：

![activity](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200304190224.png?x-oss-process=style/small)



| player_id | event_Date | devuce_id |
| --------- | ---------- | --------- |
| 1         | 2016-03-01 | 2         |
| 1         | 2016-05-02 | 2         |
| 2         | 2017-06-25 | 3         |
| 3         | 2016-03-02 | 1         |
| 3         | 2018-07-03 | 4         |



首先我们要搞到某用户某天最早登录的记录，也就是首次登录记录，由“最早”二字可以想到用MIN函数 MIN(event_date)

于是就有了SQL:

`SELECT player_id, MIN(event_date) FROM Activity `

然而这样会得到如下结果：

| player_id | event_Date |
| --------- | ---------- |
| 1         | 2016-03-01 |
| 1         | 2016-03-01 |
| 2         | 2016-03-01 |
| 3         | 2016-03-01 |
| 3         | 2016-03-01 |

这显然不是我们所想要的，我们观察此表可以发现，表中按照player_id可以分为三组，分别是1，2，3，代表着三个用户。

SQL为我们贴心准备的GROUP BY ，就是用来干这件事情的。

所以上面的SQL可以改成：

`SELECT player_id, MIN(event_date) FROM Activity GROUP BY player_id`

执行后的结果：

| player_id | event_Date |
| --------- | ---------- |
| 1         | 2016-03-01 |
| 2         | 2017-06-25 |
| 3         | 2016-03-02 |

yes!  it work !



还是上面的例子

你还可以写成`SELECT player_id, MIN(event_date) AS event_date FROM Activity GROUP BY player_id,event_date`，可以得到同样的结果

含义就由刚才1，2，3，这三个组，变成了

- 1&2016-03-01
- 2&2017-06-25
- 3&2016-03-02

每个组仍然是唯一的。

GROUP BY 的列和SELECT后面的列之间有个约束，关于解释我找到了[这篇](https://www.cnblogs.com/youzhibing/p/11516154.html)文章。

>  cname 只是每个学生的属性，并不是小组的属性，而 GROUP BY 又是聚合操作，操作的对象就是由多个学生组成的小组，因此，小组的属性只能是平均或者总和等统计性质的属性,询问每个学生的 cname 是可以的，但是询问由多个学生组成的小组的 cname 就没有意义了。对于小组来说，只有 "一共多少学生" 或者 "最大学号是多少？" 这样的问法才是有意义的。

---

接下来继续解题，有了用户们各自的首次登录记录，答案呼之欲出

## 题解

解法1:

```sql
SELECT device_id,player_id FROM Activity 
WHERE
( player_id,
  event_date
)
IN
( SELECT player_id,MIN(event_date) FROM Activity GROUP BY player_id
)
```

解法2:

```sql
SELECT a.device_id, a.player_id
FROM
Activity a
JOIN
(
SELECT player_id,MIN(event_date) lastest_date FROM Activity GROUP BY player_id
) t
ON  t.player_id = a.player_id AND t.lastest_date = a.event_date
```



我还看到有人用了下面这种解法，是真的秀，我看了挺久才想明白。

```sql
SELECT
player_id,
device_id
FROM
(
SELECT
ac.*,
if(@player=player_id,@row_num:=@row_num+1,@row_num:=1) row_num,
@player:=player_id
FROM
Activity ac,
(SELECT @row_num := 0,@player:='') b
order by player_id,event_date
) a
where a.row_num =1

作者：quan-jia-an-kang
链接：https://leetcode-cn.com/problems/game-play-analysis-ii/solution/tong-ji-de-xie-fa-by-quan-jia-an-kang/
来源：力扣（LeetCode）
```

意思就是把整个表按照 player_id 和 event_date 倒序：

| player_id‘ | event_Date | devuce_id |
| ---------- | ---------- | --------- |
| 1          | 2020-03-05 | 001       |
| 1          | 2020-03-04 | 001       |
| 1          | 2020-03-03 | 003       |
| 2          | 2020-03-03 | 099       |
| 2          | 2020-03-01 | 150       |
| 3          | 2020-03-03 | 233       |

这样相当于分成了三组，分别是

- 1组：[1,1,1]
- 2组：[2,2]
- 3组：[3]

各自的组内也是有序的，按时间倒序，所以把每一组的第一个（用row_num=1做标记）给收集起来，就是我们想要的结果集。

## 总结

以小见大，我对SQL的理解目前仅仅停留在皮毛，连一遍 [SQL标准](https://modern-sql.com/blog/2017-06/whats-new-in-sql-2016)都没认真读过，甚至连天天在用的MySQL的 [doc](https://dev.mysql.com/doc/)也没读完。。更遑论源码

幸好最近在补数据库系统原理，心里稍微舒服了点。

简单列一个重新学习数据库的todo list吧

- 数据库系统原理
- SQL标准
- MySQL
  - doc
  - 索引
  - 几个引擎的实现
- 集合论

## 后记

这篇文章并不是单纯的题解，更多的是对自己现有知识的总结，以及认识到自己的不足，写完了自己看一遍我都觉得这篇文章写的都是啥玩意。。

不过我现在不能精益求精，否则太容易打击自信了，之前就是一直觉得自己啥都不会，写的东西太腊鸡，才一直不敢写博客。

其实，不论是新手还是老手，都应该写博客。

大胆的写，干就完了！

- [ ] 