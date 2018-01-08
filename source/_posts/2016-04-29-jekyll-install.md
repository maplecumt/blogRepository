---
layout: post
section-type: post
title: 安装静态博客Jekyll
category: Jekyll
tag: tech
---
<a href="http://jekyll.bootcss.com/" title="Jekyll">Jekyll</a>是一种纯文本的静态博客，安装成功之后，直接通过markdown文本就可以更新博客内容。Jekyll的安装过程比较简单，但是安装的过程中仍然会跳进很多坑。Jekyll和<a href="https://pages.github.com/">Github Pages</a>是一种很好的结合。Github Pages是github提供的一个可以免费部署个人网站且没有存储上限的一个功能。在Jekyll的官网里也有把Jekyll<a href="http://jekyll.bootcss.com/docs/github-pages/">部署到Github Pages上的教程。</a>

## 安装Jekyll

如果需要部署到Github Pages，Jekyll需要在本地完成安装，然后再进行部署。Jekyll的安装智能在Linux和Mac OS X上进行，另外，其依赖Ruby和RubyGems，建议安装rvm来控制Ruby的版本。Linux和Mac OS X一般都会有系统自带的Ruby，但是版本比较旧，通过

<pre><code data-trim class="bash">
ruby -v
</code></pre>

可以查看当前Ruby的版本。当前Github Pages支持的是Jekyll 3.0，其依赖的Ruby 2.0及其以上版本，所以建议安装Ruby 2.0或其以上版本。
本次安装，我是直接从github上找了一个别人做好的带主题的Jekyll，然后安装在自己的VPS上了，这个Jekyll Theme的名字叫做<a href="https://github.com/PanosSakkos/personal-jekyll-theme">Personal</a>，把它git到我vps上之后，通过一个命令就可以安装完成：

<pre><code data-trim class="bash">
./scripts/install
</code></pre>

它对Ruby的需求是2.0及其以上版本，否则会安装失败。

## 配置

安装成功之后，需要对_config.yml文件进行一些个性配置。具体配置可以参考项目中的教程。主要的配置有以下几个：
- url:这个是用来指向自己的域名(如果你有的话)，配置到Github Pages上并指向自己的域名或者二级域名可以参考<a href="https://help.github.com/articles/using-a-custom-domain-with-github-pages/">github官方教程</a>
- baseurl:用来设置自己网站的相对根目录，我设置的是空，因为在我的Github Pages中的这个项目是直接放在根目录下的
- force-https:这个配置是原版Jekyll没有的，这里建议设置为false，因为Github Pages目前既支持http也支持https，如果自己没有https的证书的话，还是把其关闭的好

其余的配置都可以参考personal项目中的教程。

## 部署

配置完成之后，就可以部署到Github Pages中了，我直接把安装好的整个文件夹push到了github中。在push之前，需要先创建自己的Github Pages，每一个github用户只能创建一个Github Pages，<a href="https://pages.github.com/">这里是官方创建教程。</a>创建完成之后，把自己的文件push到根目录下，就可以通过 http://gitusername.github.io 访问了，如果设置了个人的域名，则需要到自己的域名管理网站更新域名指向，把设置的域名指向 http://gitusername.github.io 即可。需要注意的是，把自己的项目文件push到github之后，也许并不能立刻就访问到网页，也许是因为github内部需要一段时间的部署。我当时部署到github之后，立刻访问得到的是404页面，刚开始以为是自己配置出错了，过滤几个小时之后，再次访问，页面才第一次呈现。
