---
layout: post
title:  "安装 ShadowScoks"
date:   2015-11-12 15:30:00
section-type: post
category: tech
---
ShadowScoks是一个非常易用的翻墙工具，把它安装在自己的VPS上，就可以随心所欲的上网啦！
# 安装 #
输入su进入root。
分别复制以下命令到命令行：

<pre><code data-trim class="bash">
wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh
chmod +x shadowsocks.sh
./shadowsocks.sh 2>&1 | tee shadowsocks.log
</code></pre>

执行最后一条命令之后，出现一下界面：

![](https://raw.githubusercontent.com/maplecumt/maplecumt.github.io/master/images/2015-11-12-shadowsocks/ss1.png)

输入密码即可。并回车，再次回车，确认安装。

![](https://raw.githubusercontent.com/maplecumt/maplecumt.github.io/master/images/2015-11-12-shadowsocks/ss3.png)

安装失败，出现错误提示：

<pre><code data-trim class="bash ">
./shadowsocks.sh: line 111:  6396 Segmentation fault      (core dumped) apt-get -y update
Reading package lists..../shadowsocks.sh: line 111:  6461 Segmentation fault      (core dumped) apt-get -y install python python-dev python-pip curl wget unzip gcc swig automake make perl cpio
</code></pre>

分别执行 (core dumped)后面的语句

<pre><code data-trim class="bash ">
apt-get -y update
apt-get -y install python python-dev python-pip curl wget unzip gcc swig automake make perl cpio
</code></pre>

然后，重新执行:

<pre><code data-trim class="bash ">
./shadowsocks.sh 2>&1 | tee shadowsocks.log
</code></pre>

等待5分钟左右，即可安装成功，安装成功之后就会通过屏幕输出，您的IP地址，端口，密码，及加密方式。

![](https://raw.githubusercontent.com/maplecumt/maplecumt.github.io/master/images/2015-11-12-shadowsocks/ss4.png)

如果您想多用户使用，请配置 /etc/shadowsocks.json 这个文件。配置模版：

<pre><code data-trim class="ymal">
{
    "server":"your_server_ip",
    "local_address": "127.0.0.1",
    "local_port":1080,
    "port_password":{
         "8989":"password0",
         "9001":"password1",
         "9002":"password2",
         "9003":"password3",
         "9004":"password4"
    },
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open": false
}
</code></pre>

Windows客户端下载地址：[https://shadowsocks.org/en/download/clients.html](https://shadowsocks.org/en/download/clients.html)
使用教程：[http://wiki.ssnode.co/index.php?option=com_content&view=article&id=4:about-your-home-page&catid=9&Itemid=101](http://wiki.ssnode.co/index.php?option=com_content&view=article&id=4:about-your-home-page&catid=9&Itemid=101)
使用shadowsocks时，必须要通过SSH连接上自己的VPS后才能代理成功。