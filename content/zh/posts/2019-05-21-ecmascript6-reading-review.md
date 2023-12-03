---
title: 《ECMAScript6入门》读后感
date: 2019-05-21 21:21:28
lastmod: 2019-05-21 21:21:28
categories: 读书
tags:
  - es6
---

关于阮一峰《ECMAScript6 入门》一书的观感，就把此文当做本人对于《ECMAScript6 入门》的书评吧

<!--more-->

[原书链接](https://es6.ruanyifeng.com/#docs/reference)

## 暮色

首先，抛开技术不谈（这可能有点过分，一本技术书籍的书评竟然和技术没多大关系，但是秉承“一千个读者有一千个哈姆雷特”的原则，建议各位亲自去拜读此书，找寻自己的收获），当然此评也不是广告，因为阮一峰根本不认识我，我只是在学习 ES6 过程中了解到此书。再说一下为什么此文不谈技术，而更多地谈的是我看此书的感受，因为就我长期对对于阮一峰的了解和关注，他本身也认为技术只是他生活的一部分，而不是全部，令他更开心的可能是他关于人生的感想整理成书——[《未来世界的幸存者》](http://www.ruanyifeng.com/blog/2019/01/survivor-preface.html)并出版。的确，我的人生规划也不会把技术看做多么重要的东西，它只是我当下阶段职业所需的技能，我会更多地从技术中抽取不同厉害的人或深刻或缜密的思维背后的哲学，用以加深我对这个世界的认知和理解。

## 新月

阮一峰本身不是搞计算机的，他写的书却成为技术圈的参考教科书，至少在 ES6 这一个知识点上，被大家广为流传借鉴，可见学问存在“大同”效应，即大道至简。如果你是一个对于知识追求理解原理和本质的人，那么在学习了一部分知识后，自然而然会对其他未学的东西有着开导的作用。比如举个不一定恰当的例子，所谓举一反三是什么呢，在前端界我们都知道有三大主流框架 React、Vue、Angular，那放给初学者可能就觉得要学的东西太多了，竟然要掌握三种框架，去不同公司，做不同项目可能都要用不同的技术框架，简直像个学不完的无底洞。但如果是有一定经验的人会怎么看呢——举一反三，三大框架本师出同门，都是用基础语言 Javascript 经过不同的包装形式封装而成，所以高级开发经常会告诉初级工程师要打牢基础，因为基础好了，无论出现什么样的新技术都万变不离其宗，这样的学习方法就是举一反三。吃透理解一个框架，对比地再去学习另外两个，就会发现有很多相似的地方和思想，假如学习一门新技能需要花费 10 天的话，这样学起来也就不是 10x3=30 天了，而可能是 10+9+8=27 天，甚至是 10+7+3=20 天或者更少。因为伴随着你前面的积淀，再去学习新的东西，如果能利用上之前所学到的思想，大多情况下可能不会再用同样多的时间，而是越来越快，至少相近的知识是这样的。

## 月食

那么回归 ECMAScript 6 入门这本书为什么能够一直被奉为学习 ES6 入门的首推宝书呢，可能读过此书的人才能感受到。首先该书从 2014 年 4 月 20 号发生第一次 github 上的提交，在开源大家庭的共同维护下已经走过了五个年头。那为什么它会成为一本开源的书呢，作者自己当然有自己的想法，但我们也可以看到，其实阮一峰自己也经常提及自己不是计算机科班出身的事实，但这也不影响他能够写出帮助其他计算机专业的人学习的教材，也不妨碍他和技术圈的人合作产出，所以通过开源的方式，可以云集世界各地的高手一同校验、纠错，历史提交记录中不乏一些很有价值的帮助，比如“fix: [IIFE 不一定是匿名](https://github.com/ruanyf/es6tutorial/commit/eba11dd8c79819d8af9aa4ff39e35a901c0449d9)”、“[修改示例代码使其更精确](https://github.com/ruanyf/es6tutorial/commit/57fe8c62fc3c282df0dfb61156edeccc511a4815)”。另外我们可以从很多细节中感受出他对于这本书的认真态度和投入，比如最后一章所列举的参考链接，就如同专业论文的参考文献，既做到了对于参考内容的版权尊重，也帮助读者对于某些知识点的追本溯源提供了便捷的帮助。同时，这也给人一种学无止境的感觉，当你花一段时间拜读完此书时，认为自己已经做到了“ES6 入门”，然而看到最后一章附注的参考链接，才发现你刚刚打开知识海洋的大门，你会发现自己学到的只是冰山一角，因为毕竟你读完这本书可能只要花费不到一个月的时间，而作者写成这本书却要花费五年的心血，甚至更多。所以说——学无止境，任何时候你感觉自己已经会了，或者对于某个领域或某个知识点完全理解了，都是在阻碍你后面更大的进步。

## 破晓

再说一个令人咂舌的细节点，就我写下此评的这一天（2019 年 05 月 21 日 17:27:02）打开该书的 github 地址，发现[issues](https://github.com/ruanyf/es6tutorial/issues)和[pull requests](https://github.com/ruanyf/es6tutorial/pulls)栏目的待审阅数双双为零，乍一看还以为是此书封版了，已经完善归档，不再需要更新，或是作者设置为禁止其他人继续提交改动了，但好像不是这样。点开近期 close 掉的 issue，发现刚发生在 3 天前，同时最近一次的 pull request 处理于 4 天前，看到这个足以令人震惊。因为逛开源圈的都知道，茫茫众多开源项目，能够做到这样及时关注用户反馈，对开源提交做出处理，达到 0 待处理 issue 和 0 待处理 pr 的开源项目实在不多，这有时也是从维护积极性维度衡量一个开源项目质量高低的核心指标，有些开源项目一开始很好，比如框架或者工具类的项目，大家会当做现成轮子去使用到生产中，但时过境迁，当项目中所使用的开源工具出现问题，由于是开源项目，所以项目作者就是项目的售后和客服，遇到问题了，如果从网上找不到太大的帮助，八成会回到 github 的项目原地址来看看 issue 或者 pr 中别人有没有睬过同样的坑，当欣喜若狂地搜索到结果后，迎面而来的可能是一盆冷水，就是这种问题的确也很多人遇到过，但作者已经很久没有再维护此项目了，issue 和 pr 中待处理的问题一堆，逐渐地人们可能会换用其他新的技术框架或方案，这样的开源项目便也就此论为昙花一现。与之不同的是，阮一峰能够持续地维护此书，的确值得钦佩。可能有人会说，这只是一本小书，文字内容为主，附以简单的代码片段说明，跟大的开源技术框架不能比，但我们这里看到的是态度，一个人对于小的事情能够报以认真严肃的态度，当面对大问题的时候大多能够从容应对，毕竟还有分治策略不是吗，大的问题大多可以拆解成多个小的问题的合集，继而分而治之。就好比一个人从刚入职场做着简单的岗位起，如果因为觉得基础岗位所做的事情简单无趣而不能认真对待，那么怎么能够得到晋升去做更大事情的机会呢，相反能够在基础岗位做出优异成绩的人大多稳步发展，逐步上升，成为厉害的人，这才是我们应该学习的态度。千里之行始于足下、高楼万丈平地起，这样的道理我们从小学时期就受过教育，只是很多人在成长的过程中都丢掉了。