---
title: 关于反向代理的整理
date: 2017-11-07 16:41:24
lastmod: 2017-11-07 16:41:24
tags: ["Web"]
---

之前一直对**反向代理**这个概念理解的很模糊，网上参阅了很多解释，看完也是觉得不够信服，相比较而言觉得解释的还算良好的是知乎上看到的一个[回答](https://www.zhihu.com/question/24723688)，但看了之后也仅限于“当时理解，过后就忘”，于是今天再次在 stackoverflow 看到的解释版本，特此翻译整理，留作备忘。

<!-- more -->

原文链接：<a href="https://stackoverflow.com/questions/224664/difference-between-proxy-server-and-reverse-proxy-server/366212#366212">https://stackoverflow.com/questions/224664/difference-between-proxy-server-and-reverse-proxy-server/366212#366212</a>

如果当你访问不了这个链接的时候，也就说明，GFW 限制了大陆网络内的主机访问 stackoverflow 的网站内容，此时你即需要通过**代理服务器**来作为你的代理，帮你取拿到远端 stackoverflow 网站上的内容取回给你，这就是正向代理的使用实例。

而反向代理其实更常见，因为它充斥在我们每一天的网上冲浪之中，**只不过你意识不到罢了**（注意！这也就是正向代理和反向代理很大的特征区别之一：正向代理需要你去寻得一个代理来帮助你访问你访问不了的服务器资源，而反向代理是服务器端使用的代理，来处理你提交的访问请求，所以作为客户端的你是意识不到代理的存在的）。

比如你通过浏览器访问百度网搜索一个条目，或者直接在地址栏输入 stackoverflow.com，然而这个行为在互联网中有太多用户在做，所以百度或者 stackoverflow 的服务器不一定能够驾驭这么大的访问量，此时他们可能会把相同的服务部署在 N 多台服务器节点上，然后你其实访问到的是那些提供反向代理的服务器，反向代理服务器将大量的请求做了负载均衡处理，再把这些请求均衡合理地分配到那些提供相同服务的不同服务器节点上，这就是反向代理的实例。

接下来是本人对于 stackoverflow 上精彩回答的翻译，如有不准确之处请指正

> 前面的回答都很准确，但可能太过于精简了。我会试着增加一些例子。
> 首先，“代理”这个词描述了某个人或者某个事物扮演着代表另一个人的角色。在计算机领域，我们讨论的即是一台服务器扮演着代表另一台计算机的角色。为了保证观点可达性（即观点可以被很容易的理解）这一目的（这句感觉翻译的不太好），我会限制我的讨论仅限于“web 代理”，然而“代理”这一思想其实不仅限于 web 网站。

## 正向代理

> 大多数关于 web 代理的讨论都指的是"正向代理"（这句感觉翻译得不甚准确）。这种情况下的代理事件其实就是“正向代理”代表请求者从另一个 web 站点取得数据。

> 举个栗子，我会列举三台接入互联网的计算机。

> X = 你的计算机，或者说互联中的“客户机”

> Y = 代理站点，proxy.example.org

> Z = 你想要访问的网站，www.example.net

> 通常，你可能是类似 X --> Z 这样的直连。

> 然而，在一些场景下，Y --> Z 来代表 X（去访问 Z）更好，链条如下：X --> Y --> Z

> 为什么 X 需要使用代理服务器的原因：

> X 无法直接访问到 Z:

> a)在 X 的互联网连接中某个拥有管理权限的人决定拦截所有 X 到 Z 站点的访问（比如 GFW : ) ）

> 实例：

> 1. 风暴蠕虫病毒蔓延，它欺骗人们去访问 familypostcards2008.com，所以系统管理员封锁了对于这个网站的访问来保护用户们以避免其因为不小心而感染病毒。

> 2. 一家大型公司的员工花费了太多的时间用在 facebook.com 的访问上，所以管理者想要这些访问在工作时间被屏蔽掉。

> 3. 一家当地小学禁止了其对于 playboy.com 这个网站的互联网访问

> 4. 政府无法控制人们发布新闻，所以它控制了新闻的访问取而代之，通过封锁类似 wikipedia.org 这样的网站，更多请查阅**<a href="http://www.onion-router.net/">TOR</a>**或者**<a href="http://freenetproject.org/">FreeNet</a>**

> b) Z 点的管理员禁止了来自 X 的访问

> 实例：

> 1. Z 站点的管理员被告知可能存在来自于 X 的黑客攻击尝试行为，所以管理员决定禁掉 X 的 IP 地址（<a href="http://www.netrange.com/">http://www.netrange.com/</a>）

> 2. Z 是一个论坛网站，X 正在该论坛刷屏。Z 禁掉了 X。

## 反向代理

> X = 你的计算机，或者说互联中的“客户机”

> Y = 反向代理站点，proxy.example.org

> Z = 你想要访问的网站，www.example.net

> 通常，你可能是类似 X --> Z 这样的直连。

> 然而，在一些场景，对于 Z 的管理员限制掉或者不允许这样的直连更好，同时强迫访问者先去访问 Y。所以，如同往常，我们通过 Y --> Z 代表 X 取得想要访问的数据，链条如下： X --> Y --> Z

> 相比“正向代理”不同的是，这次用户 X 并不知道他在访问 Z，因为他只能看到他在和 Y 通信。Z 服务端对于客户端来说不可见并且只有反向代理 Y 对于外部是可见的。所以一个反向代理是不需要在客户端做配置的。

> 客户端 X 认为他只是在和 Y 进行通信（即 X --> Y），但事实上是 Y 在传导所有的通信（再一次成为 X --> Y --> Z 这样的通信结构）

> 为什么 Z 想要设置一个代理服务器的原因：

> 1）Z 想要强迫所有对于它的通信访问都先经过 Y。
> a)Z 有一个成千上万人想要访问的巨大 web 站点，但仅仅一个 web 服务器不能处理所有的网络请求。所以 Z 架设了许多许多的服务器，并在互联网放置一个反向代理，以便当用户想要访问 Z 的时候把他们的访问请求派发到离他们最近的服务器去。这也是**内容分发网络**（CDN）概念如何工作的一部分。

> 实例：

> 1. <a href="http://trailers.apple.com/trailers/">Apple Trailers</a>使用<a href="https://www.akamai.com/">Akamai</a>

> 2. Jquery.com 使用<a href="http://aws.amazon.com/s3/">CloudFront CDN</a>来存放它的 javascript 文件（例如：<a href="http://static.jquery.com/files/rocker/scripts/custom.js">sample</a>）

> 3. 等等

> 2）Z 的管理员担心来自于对其网站内容的报复行为，并且不想直接向大众暴露其主服务器。

> 1. 类似"Canadian Pharmacy"这样的垃圾品牌的拥有者看上去拥有成千上万的服务器，然而实际上它大多数网站都只部署在比看上去少得多的服务器上。另外，关于刷屏的 abuse complaints 实际上只会关掉那些公共服务器，而非主服务器。

> 最后这段实在无力翻译，自己都看着难受 :(

> 在如上的场景，Z 决定选择 Y（作为反向代理）
