---
title: "周报"
tags: [thoughts]
---

始于 22.7.31

<!--more-->


<details>
  <summary>22.7.31 - 22.8.6</summary>

本周原计划是准备秋招，在周一干完了能应付一周的活后，周二突然来了个很急的需求，要求本周内完成，秋招的事就只能先放放了。

这个需求非常 CRUD，需要从服务器日志中解析出所有的用户 id，调用 rpc 接口去查询用户的更多数据，最后把数据通过 api 插入到 OLAP 数据库。

最终顺利在周五完成需求，事后总结有几点收获：

* 动态语言挺好用。setattr 能对库的类增加成员函数，减少很多冗余代码。不过对于其他语言，用 trait 也能满足我的需求
* 类型系统很重要，py 应该强制要求类型标注。内部库有一个函数调用类型匹配错误的 bug，该代码之前没被调用过，藏匿至今，不可思议。要是有类型标注，不致于此。想起之前跟面试官介绍 mypy 项目的被鄙夷的场面了
* 库函数向用户通知错误的方式，除了错误码就是抛出异常。这次的需求用 py2 编写，我采用抛出异常的方式，在主函数 catch 异常并写入日志，极大降低理清程序逻辑的心智负担，避免错误码层层传递，深刻感受到异常控制流的威力
* 以下代码并不等价
```
try:
    count += 1
except:
    count += 1
```

```
try:
    pass
except:
    pass
finally:
    count += 1
```
* 序列化反序列化意外地非常耗时。之前读 ddia 有这么一段话，大意是，内存数据库更快的原因不在于数据是存放在内存中，而是因为免去了数据打包解包的过程。如果内存足够大，基于磁盘的数据库也可以不需要磁盘 IO。当时将信将疑，现在总算见识到了
* 在思考业务的边界情况时，总结了一些方法论。比如函数的语义最好写成纯函数，逻辑性的 bug 通常出现在有副作用的变量上，需要着重关注有副作用变量经过的控制流，以及与该变量有关联的其他副作用变量。总结得还不太完善。我觉得形式化验证是不是就在关心这方面的工作，有空了解一下
* 公司内部的工具链太老了，吐槽已久。正好周一读了这篇[博文](https://xuanwo.io/reports/2022-25/)，有了更深的体会
</details>



<details>
  <summary>22.8.7 - 22.8.21</summary>

这两周在准备面试的东西，快速复习之前的笔记，发现好多细节都忘记了，可惜没太多时间去温习，只能走马观花，感觉有点手忙脚乱，不知道要干嘛了。

到目前为止投了 13 家公司，有回复的只有四家。简单记录接下来的安排

- [x] 13 号华为一二面
- [x] 14 号大疆笔试
- [x] 18 号寒武纪电面
- [x] 20 号华为主管面
- [x] 22 号转正相关工作

17 号刷脉脉时发现之前参加开源项目眼熟的大佬在发内推帖，加微信发了自己的简历。他看完提一口不很偏数据库。我自己心知肚明，但还是很沮丧。总结这几年的学习生涯，自己东学一点西学一点，蜻蜓点水，没有真正专注于一个领域去深挖。深感自己太菜了，眼界也狭窄。看了看大佬们的博客，整理了之后要学习的东西（接下来大概得毕业论文写完才有空了吧）。目前还是看看 leveldb，应付一下面试再说吧。

<details>
  <summary>TODO List</summary>

要读的书

- [ ] Readings in Database Systems
- [ ] 精通 LevelDB
- [ ] MySQL 技术内幕：InnoDB存储引擎
- [ ] 数据库查询优化器的艺术：原理解析与 SQL 性能优化
- [ ] 阅读[风空之枫的书单](https://github.com/mapleFU/MySQL-eight-legged)

要读的论文

- [ ] [C-Store: A Column-oriented DBMS](https://web.stanford.edu/class/cs345d-01/rl/cstore.pdf)
- [x] [Wisckey](https://www.bilibili.com/read/cv13658411)、 [参考资料](https://www.zhihu.com/column/c_1452633136869416960)
- [ ] [卡比卡比的知乎专栏](https://www.zhihu.com/column/c_1440347225616953344)

要研究的项目

- [ ] boltdb [参考资料](https://zhuanlan.zhihu.com/p/391693148)
- [ ] TinyKV
- [ ] TinySql
- [ ] kvrocks

</details>

</details>

<details>
  <summary>22.8.22 - 22.8.28</summary>
  
22 号公司的转正通知下来了，leader 跟我说整个工作室都没 hc 可以转正。那也是没办法的事，遇上了就是遇上了，没办法就是没办法。

23 号看了篇[博文](https://www.tisonkun.org/2022/08/22/github-for-hrs/)，深感还是得多提高自己的影响力，多参与开源。

这周确定没 hc 后就光明正大摸鱼了。周三下午连续三场面试车轮战很累，寒武纪面得不好，领域知识确实不足。selectdb 面试体验极佳，上次这么聊得来的还是春招蚂蚁一面。蔚来面得中规中矩，一面挂有点意外。周五 selectdb 二面，面试体验也很好，希望能有好的结果。

- [x] 24 号寒武纪二面
- [x] 24 号 selectdb 一面
- [x] 24 号蔚来一面
- [x] 25 号学校中期答辩
- [x] 26 号 selectdb 二面
- [x] 27 号美团笔试
- [x] 26 号 selectdb 二面
</details>


<details>
  <summary>22.8.29 - 22.9.4</summary>
selectdb 二面挂，遗憾。目前投了二十多家，还没有一个 offer，感觉已经很久没有发生好的事情了。现在相比春招时硬气不少，但面试还是没过，意识到自己应该在某个专业领域持续投入，这周找几篇论文开始看了，也开始做 cmu15445 的实验。不过在周五的时候，在群里看到搞静态分析的真大佬也投了 selectdb，和我也是同个面试官，这下对比很明显了，泪目。大佬很顺利，offer 30K。据我所知他好像也没搞数据库，我开始动摇了，也许面试更看重的不是专业知识，而是开源贡献？
  
大疆面试时问了访问者模式，我前段时间在写数据库时就遇到这个问题并心里总结一下，但是面试时记不清了。现在记录如下：

* 根据不同派生类执行不同操作，比如说 Binder 将 AST 转成 Bound 的场景。Binder::bind 函数输入参数是 AST 基类指针，需要根据不同派生类做对应操作。

1. Binder 直接调用 AST 虚函数，由 AST 派生类的虚函数生成对应的 Bound 派生类。可以，但是我们希望将执行的过程从 AST 类中抽离到 Binder 中。因为在某些场景，执行的内容从逻辑上讲并不是 AST 的功能
2. 给 AST 加入 tag，根据 tag 来获取派生类的类型，并将 AST 基类指针转成派生类。可以，但不优雅。
 * 构造 AST 派生类需要定义 tag 值，而且 bind 中需要判断 tag 进行分发。而且继承树很深的情况下，需要判断很多次 tag（Statement-Expression-Value-StringValue）
 * raw 基类指针转成派生类指针很容易，但是基类智能指针转成派生类智能指针有点麻烦
3. 使用访问者模式。bind 调用指针的虚函数，虚函数调用 Binder 对应的函数。这函数一般都是重载函数，由参数匹配选择对应的重载函数。
4. 考虑到访问者模式调用链复杂，bind 直接调用由参数匹配选择对应的重载函数。不可以，因为基类指针不能自动向派生类转换。  
* 派生类的虚函数返回不同类型，基类的虚函数返回值如何定义？比如基类 Value，派生类 StringValue、IntValue，虚函数 GetValue()
1. union
2. variant，最好配合 visit 一起使用 [参考](https://zhuanlan.zhihu.com/p/366537214)


- [x] 29 号字节一面
- [x] 1 号大疆一面
- [x] wisckey 论文
- [ ] An Overview of Query Optimization in Relation Systems
- [ ] Differentiated Key-Value Storage Management for Balanced I/O Performance，[参考](https://www.scienjus.com/diffkv/)
- [ ] [数据库学习经验杂谈（长期更新）](https://zhuanlan.zhihu.com/p/553503630)
</details>

<details>
  <summary>22.9.5 - 22.9.25</summary>
这周所有事都凑一起，疫情封城边缘，离职办理，出租屋到期，笔试面试，电脑坏了，打乱太多计划。不过最后还是都 handle 了，只是花了不少钱。

在家隔离了几天，除了笔试面试，没怎么学习。

17 号回校。

回校一周一直看 eac 这本书，也记了几篇笔记，感觉很好。


</details>