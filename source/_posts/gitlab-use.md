---
title: 服务器搭建Gitlab
date: 2018-08-27 09:30:00
tags:
---

# 服务器搭建Gitlab

> 创作于2018年左右，最初创建时间已丢失

## 环境

- ubuntu16.04

## 安装gitlab-ee步骤(无特殊说明，安装过程中采用默认配置项)

1. 安装和配置必要依赖

```
sudo apt-get update
sudo apt-get install -y curl openssh-server ca-certificates
```

2. 安装邮件服务器

```
sudo apt-get install -y postfix
```

3. 下载gitlab安装包并安装

```
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.deb.sh | sudo bash
```

4. 设置访问路径(此处有坑)

```
sudo EXTERNAL_URL="http://gitlab.example.com" apt-get install gitlab-ee
```

这里的方式是在安装gitlab企业版的命令上通过参数的方式指定访问地址，官网示例中直接给的是一个域名地址，此操作其实会在gitlab安装后的`/etc/gitlab/gitlab.rb`文件里有个`EXTERNAL_URL`的配置项（整个gitlab的所有配置都在此）

所以当然这里也就可以只进行安装，即

```
sudo apt-get install gitlab-ee
```

然后再修改默认的配置文件，把`EXTERNAL_URL`改成gitlab的访问地址

```
vi /etc/gitlab/gitlab.rb
```

重新加载配置文件

```
sudo gitlab-ctl reconfigure
```

重启gitlab服务

```
sudo gitlab-ctl restart
```

问题来了，如果你这里`EXTERNAL_URL`配置为机器的IP，即

```
EXTERNAL_URL="http://xx.xx.xx.xx"
```

那么默认访问的是`http://xx.xx.xx.xx`的80端口，而80端口可能被占用，或受ECS限制，需要单独配置80端口的访问权限，所以这里可以自定义访问的端口，方法也很简单，就是在IP地址后面加上端口，例如：

```
EXTERNAL_URL="http://xx.xx.xx.xx:8800"
```

然后还有关键的一步，就是开放端口对外的访问权限，这里以ubuntu16.04为例

安装iptables
```
sudo apt-get install iptables
```

添加规则
```
iptables -I INPUT -p tcp --dport 8800 -j ACCEPT
```

保存规则
```
iptables-save
```

这样操作后，服务器重启后会失效，需要持久化规则


安装iptables-persistent
```
sudo apt-get install iptables-persistent
sudo netfilter-persistent save
sudo netfilter-persistent reload
```

5. 初始化账号

访问配置好的gitlab地址，例如`http://xx.xx.xx.xx:8800`，会提示设置密码，这里设置的即是管理员root的密码，重设后使用如下账号登录管理员账号

用户名：root

密码：重设后的密码

6. 初始化组、用户、项目

创建一个group，点击顶部扳手图标（admin area），添加用户，添加用户后保存，然后再通过Edit修改可设置初始密码（用户使用该账号登录后会提示修改密码）

7. 将用户添加进组，创建项目

8. 用户初始操作

登录gitlab地址，点击Setting，添加本地已有的或生成的SSH-KEY

9. 完成

## 卸载gitlab-ee

这才是个大坑，比安装麻烦（卸载干净不容易），官网也没找到官方的卸载步骤

还好*nix系统秉承一切皆文件，并且提供了一系列强大工具，比如ls、find、grep，可以全局查找进行手动清理

1. 停服务

```
sudo gitlab-ctl stop 
```

2. 进程操作（可选）

查看进程
```
ps -ef|grep gitlab
```

找到守护进程`runsvdir -P /opt/gitlab/service log`的PID并停掉

```
kill -9 端口号
```

3. 删除gitlab相关文件

```
find / -name gitlab |xargs rm -rf 
```

4. 删除包含gitlab的相关目录和文件

```
find / -name *gitlab*|xargs rm -rf
```

5. 删除uninstall时生成的备份文件（可选）

```
ls /root/gitlab*
rm -rf /root/gitlab*
```

6. Done

## 安装gitlab-ce

1、2步同企业版(简略如下)

```
sudo apt-get install curl openssh-server ca-certificates postfix
```

3. 下载gitlab-ce包

```
curl -O https://downloads-packages.s3.amazonaws.com/ubuntu-14.04/gitlab_7.4.2-omnibus-1_amd64.deb
```

4. 或者直接下载安装脚本

```
curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash
```

5. 上面的脚本执行后会添加gitlab服务器配置到`/etc/apt/sources.list.d`目录，并且添加配置文件`gitlab_gitlab-ce.list`到`/etc/apt/sources.list.d`目录，内容如下

```
# this file was generated by packages.gitlab.com for
# the repository at https://packages.gitlab.com/gitlab/gitlab-ce

deb https://packages.gitlab.com/gitlab/gitlab-ce/ubuntu/ xenial main
deb-src https://packages.gitlab.com/gitlab/gitlab-ce/ubuntu/ xenial main
```

可通过`more /etc/apt/sources.list.d/gitlab_gitlab-ce.list`查看

> 后缀为deb的为包，使用curl -O 下载到本地当前文件夹，名称为deb包的文件名，使用`-o`参数可以自定义下载到本地的文件名，例如`curl -o mygettext.html http://www.gnu.org/software/gettext/manual/gettext.html`，后缀为deb.sh的为安装脚本，需要通过管道调用bash来运行安装脚本，例如`curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.deb.sh | sudo bash`

6. 安装gitlab-ce

```
sudo apt-get install gitlab-ce
```

7. 修改配置文件，把`EXTERNAL_URL`改成gitlab的访问地址

```
vi /etc/gitlab/gitlab.rb
```

8. 重新加载配置文件

```
sudo gitlab-ctl reconfigure
```

9. 重启gitlab服务

```
sudo gitlab-ctl restart
```

10. 其他操作见企业版安装（比如开放外部访问端口等）

11. 访问配置好的地址

12. 账号初始化

## 参考链接

- [gitlab官方文档——安装篇](https://about.gitlab.com/installation/#ubuntu)
- [ubuntu开放指定端口](https://www.jianshu.com/p/2ec5d16db02b)
- [使用本地已有ssh-key或生成ssh-key](https://docs.joyent.com/public-cloud/getting-started/ssh-keys/generating-an-ssh-key-manually/manually-generating-your-ssh-key-in-mac-os-x)
- [社区版gitlab部署](https://www.cnblogs.com/restran/p/4063880.html)
- [gitlab论坛关于卸载gitlab社区版](https://forum.gitlab.com/t/complete-uninstall-gitlab-ce-from-ubuntu-14/6232/2)
- [CentOs 7 安装 GitLab、完全卸载GitLab](https://blog.csdn.net/huhuhuemail/article/details/80519433)
- [Ubuntu16.04安装gitlab-ce](https://beginor.github.io/2016/05/07/gitlab-ce-installation-record.html)