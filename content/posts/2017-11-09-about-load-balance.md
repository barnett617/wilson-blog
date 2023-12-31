---
title: 关于负载均衡的理解小结
date: 2017-11-09 17:37:16
lastmod: 2017-11-09 17:37:16
tags: ["OS"]
---

均衡，存乎万物之间

<!-- more -->

负载均衡（Load Balance）是指将请求**均匀**分摊到多个操作单元上执行，关键在于**均匀**

本来在学习过**反向代理**这个概念以后以为负载均衡就是反向代理在服务端将来自客户端短时大量的访问请求做分发，将其分配到多台提供相同服务的服务器上。
看了负载均衡以后发现其实**负载均衡**是一个很宏观的概念，上述的理解存在一定偏差。

负载均衡旨在将特定的业务分担给多个服务器或网络设备，从而提高业务处理能力，保证业务的高可用性。

（负载均衡用于缓解极大量的访问请求，所以下面的场景都基于同时来自客户端大量的访问请求）

首先，我上面的理解在实际的负载均衡中其实表述的是【DNS 层】（客户端->反向代理层）的负载均衡，这一层的负载均衡由 DNS 服务器实现。

具体也就是当用户通过网站域名访问服务时，为了**负载均衡**，同一域名会配置多个解析 IP，每当 DNS 解析请求来访问 DNS 服务器时，它会轮询这些 IP，并保证每个 IP 的解析概率相同（均匀），这些 IP 就是 nginx 的外网 IP。

然后拿到某台 nginx 的 IP 也就结束了第一层的负载均衡

接下来，来到【反向代理层—>站点层】，这一层的负载均衡通过 nginx 的配置实现，策略有很多种：比如轮询、IP 哈希、URL 哈希、权重等

1. 请求轮询：类似 DNS 轮询，请求依次被路由到每一个 web 服务器

2. 最少连接路由：将请求路由到连接数最少的 web 服务器

3. IP 哈希：通过客户端 IP 的哈希值来路由到某一个 web 服务器（只要用户 IP 分布均匀，理论上路由的路径就是均匀的），这样同一个用户的请求会固定路由到固定的某一台 web 服务器上，该策略适合有状态服务，比如 session（但不建议这么做，因为站点层无状态是分布式架构设计的基本原则之一，session 最好放在数据层存储）

然后是【站点层->服务层】的负载均衡，该层通过服务连接池实现

上游连接池与下游服务建立多个连接，每次请求会“随机”选取连接访问下游服务

最后是【数据层】负载均衡

当数据量十分庞大的时候，数据层（db，cache）可能会进行数据的水平切分，于是该层的负载均衡包含“数据均衡”和“请求均衡”两部分

数据均衡指：水平切分后的每个服务（db，cache），彼此之间**数据量**均匀

请求均衡指：水平切分后的每个服务（db，cache），彼此之间**请求量**均匀

常见水平切分法如下：

1. 按照数据范围切分：每个数据服务存储一定范围内的数据

DataServiceA：存储 uid 为[1-1kw)内的数据
DataServiceB：存储 uid 为[1kw-2kw)内的数据

优点：

- 规则简单，来自服务层的访问仅根据 uid 范围即可路由到对应的存储服务

- 数据均衡性良好（除最后一份，其他均为等分）

- 易拓展，可随时添加 uid 为 2kw 以后的数据服务

缺点：

- 请求均衡不一定到位，例如新注册的用户会比老用户更活跃，即 uid 数值大的服务请求压力更大

2. 按照 ID 的哈希值切分：每个数据服务存储 uid 哈希后的**部分数据**

DataServiceA：存储 uid 哈希后的部分数据
DataServiceB：存储 uid 哈希后的另一部分数据

优点：

- 规则简单，来自服务层的访问仅根据 uid 进行哈希计算即可路由到对应的存储服务

- 数据均衡性良好

- 请求均衡性良好

缺点：

- 不易拓展，拓展一个数据服务时，哈希方法改变，可能需要进行数据迁移

总结：

各层负载均衡实现方式

【客户端->反向代理】：DNS 轮询

【反向代理->Web 站点】：nginx

【Web 站点->服务】：服务连接池

【服务->数据】：数据均衡+请求均衡

参考链接：[一分钟了解负载均衡](http://developer.51cto.com/art/201609/517313.htm)
