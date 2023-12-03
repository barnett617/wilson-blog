---
title: 博客重新更新了
tags:
  - 其他
date: 2020-05-02 18:36:54
lastmod: 2020-05-02 18:36:54
categories: 总结
---

时隔许久，决定重新打开尘封许久的博客。

<!--more-->

很久没再更新，一方面是因为曾一度觉得在某些问题的解决上，网上其他人写的更有价值，也就不想再生产“网络垃圾”，另一方面是项目多起来真的很难有时间拿来写博客，往往一个项目结束，正想着复盘整理一下项目中的收获和疑点时，下一个项目就又开始了。

这次借着疫情期间闲下来，决定重新捡起这个东西。

---

## 换个博客主题

第一步想到的是要换个博客主题，博客本身是基于 [Hexo](https://hexo.io/zh-cn/) 引擎的，其 [主题列表](https://hexo.io/themes/) 也是百花齐放，质量层次不齐，并且数量还在不断增加中，很难从中选到一个中意的。再三对比下我选择了既简洁又不失美观的 [fluid](https://github.com/fluid-dev/hexo-theme-fluid)，应该是截至目前我最满意的主题了。它是基于 [material](https://github.com/bolnh/hexo-theme-material) 设计风格的，和它类似的另一款主题是 [matery](https://github.com/blinkfox/hexo-theme-matery) ，也是我之前用的主题，现在再看感觉过于花哨，功能虽多，但看上去过于炫技，反而丧失了博客的本质——文字记录。相比之下，fluid 的首页排版会让我觉得更加聚焦于博客列表的展示，其实这我都觉得有点花哨，因为主题出于美观的目的导致布局中的间距有点大，首页能够展示的博客数不够多。起初我是想这次做成 [jjc](https://justjavac.com/) 和 [颜海镜](https://yanhaijing.com/) 两位大神那样的风格，就简简单单首页陈列所有的博客标题，没有多余的东西。但后来想想还是算了，毕竟自己还没到那么成熟的段位，可能驾驭不了那么成熟稳重的风格，自己的博客中还是需要一些活力的元素，于是便选择了这个介于浮夸和稳重之间的主题风格。

## 为什么重新解封博客

这次重新捡起博客的另一个重要原因是想整合之前写过的所有文字记录，因为感觉平时自己也写过一些自认为比较有意义的东西，有些是学习工作过程中对于问题解决的记录，有的是学习到不同阶段所产生的感悟，有些纯粹是为了记录某些东西便于后续查找的。

总之，有很多东西需要被汇总到一起。

因为平时有的东西可能随手一写就放在电脑本地了，有的在笔记本里的，有的在台式机里，还有一些是在没有独立博客前散落在各种公共博客空间写的。我觉得出于对自己所生产内容负责的态度，这些产出应该被比较完整地去维护。比如之前本地随笔写的东西可能很多因为没有发出来就烂尾了，而如果有这样一个长期维护的博客，可能会起到一个督促自己的作用。所以这次想借着重新开启博客的机会，把之前这些有想法但没落实的事做一做，也算给自己一个阶段性的交代。

## 这次做了什么

首先，回顾了一下自己博客的部署方式，我是在 [coding](https://coding.net/) 存储博客的源项目，然后博客编译出的静态文件部署在 coding 的另一个仓库，还有之前用的主题 [matery](https://github.com/blinkfox/hexo-theme-matery) 作为一个 git 子模块放在项目内，同时它也单独存放在一个 coding 仓库内，所以一共三个仓库。这样我在任何一台电脑都可以下载源文件进行博客发布，这是之前研究 [博客备份](http://www.h2mes.com/) 留下来的方案，因为之前有过因为没有对源文件进行 git 管理而导致换电脑后无法继续发博客的惨案。

其次我在选择博客主题的时候发现 hexo 有很多比较好的周边项目，比如它有自己的 [cli](https://github.com/hexojs/hexo-cli) 于是就先去看了一下 hexo 的源码，发现有一个比较活跃的团队在维护着 [hexo](https://github.com/hexojs) 这一系列项目，比如用新的 ES 特性更新了框架内部的很多实现。而且其主题列表也有很多自由开发者在不断贡献自己的作品，以供更多人选择，总体算是一个比较完善的博客引擎。和它类似的博客引擎应该就是 [jeklly](http://jekyllbootstrap.com/) 了，也就是 jjc 和 颜海镜 两位大神的选择。这应该是比较早的博客引擎，基于 bootstrap 的。Bootstrap 大家应该都知道，很早的 UI 框架了，所以 jeklly 也算是上一批的博客引擎。甚至我感觉 hexo 就是国人参考 jeklly 用 node 重写出来的。jeklly 是基于 perl 的，所以相比而言对于 “新前端人” 没有 node 那么熟悉，可能这也成为 hexo 更流行的原因吧。

列举一些我觉得比较好的主题：

- 经典主题 [next](https://theme-next.iissnan.com/) 应该是很多 hexo 用户去掉默认主题后用的第一个主题
- 左右排版的 [yilia](https://github.com/JoeyBling/hexo-theme-yilia-plus) 应该也算比较经久耐用的老主题了
- 很有冲击力的 [butterfly](https://github.com/jerryc127/hexo-theme-butterfly) 是很多人的选择，我也挺喜欢的，但是图片元素太多，会压过文字内容的风头
- [matery](https://github.com/blinkfox/hexo-theme-matery) ，我的前主题，功能大而全，最大的缺点就是功能太多了，适合尝试，不适合久用

好了，记录好这些可以留作备用的主题，我项目中的这些主题文件也就可以删掉了。

最终让我决定使用 fluid 是因为 [Fluid 发布 1.8.0 版本，优雅与简约共存的主题](https://www.v2ex.com/t/667921) 这个帖子。这个主题维护的比较好，而且审美兼具美观与大气，是让我觉得比较中意的。

## 写在最后

对于博客内容这个东西，不管好的坏的，都是自己曾经写的。历史不应该被遗忘，也不应该被篡改。

可能每过一个阶段再去看曾经的自己会觉得幼稚不堪，但没有那时的自己，怎么会有今天的自己，反而有这样一份“日记”当作写照不也正是在正视自己成长过程中的每一个阶段么。

每一个大神也都曾是萌新。