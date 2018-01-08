---
layout: post
title:  "Ubuntu用户设置"
section-type: post
date:   2015-12-01 12:00:00
category: Ubuntu
tag: tech
---
最近在安装实验室一台服务器，系统装的是Ubuntu 14.04，今天在添加用户的时候出了点小问题，在这里总结一下。

# 为Ubuntu添加新用户 #
在网上查到为Ubuntu填加新用户的方式是 sudo useradd me和passwd me来设置，但是，这样设置有一个很大的坑，因为这样设置的用户信息是不全的，直接导致使用这种方式设置的用户在进行远程登陆的时候，会出现

```
    Could not chdir to home directory /home/me: No such file or directory
```

的错误，可以用过输入 bash 来进入正常的状态

```
    $ bash
    me@server:/$
```

为了解决这个问题，其实就是修改用户的默认shell为bash。去Google了一番，终于找到解决方案：
[http://askubuntu.com/questions/28969/how-do-you-change-the-default-shell-for-all-users-to-bash](http://askubuntu.com/questions/28969/how-do-you-change-the-default-shell-for-all-users-to-bash "点击这里查看（Jack O'Connor的答案）")。
方法就是，如果是root用户：

```
    usermod -s /bin/bash USERNAME
```

如果不是root用户：

```
    sudo -u USERNAME chsh -s /bin/bash
```
走过这个坑之后，建议以后添加用户，换成另外一种方式， sudo adduser me，这样虽然麻烦一些，但是权限和信息都是更加完整的。

# 为用户添加root权限 #
为了能使用root权限，又去搜索了一遍如何为用户添加root权限，这里有一篇文章讲解的很详细[http://blog.csdn.net/dreamback1987/article/details/8766302](http://blog.csdn.net/dreamback1987/article/details/8766302 "用户不在sudoers里")。这里的关键点就是在修改 /etc/sudoers文件前，需要修改它的权限，改完保存之后，再把文件权限修改回来，因为如果 /etc/sudoers 文件的权限为 777 的话，sudo命令就不能使用了。

# root用户和普通用户来回切换 #
因为本人菜鸟一枚，这里记录一下刚刚学到的一个小命令，就是root用户和普通用户的来回切换：

```
    $su root		#切换到root用户
    $su me			#切换到me用户
```
