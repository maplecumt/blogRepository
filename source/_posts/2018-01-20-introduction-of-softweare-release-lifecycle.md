---
layout: post
section-type: post
title: 软件开发生命周期
category: Tech
tag: IT
date: 2018-01-20
---
![](https://raw.githubusercontent.com/maplecumt/blogImages/master/introduction-of-software-release-life-cycle/software-release-life-cycle.jpg)
<!-- more -->
# 前言

最近研究React的时候，看到这样一个版本号 React 16 RC，非常疑惑，不知道这里的RC到底是什么意思。

# 软件版本周期

查了相关资料才知道，这个和软件版本周期有关，然后在Wikipedia里找到了这张图，这是经过优化过的，原图比较丑`^_^`。

![](https://raw.githubusercontent.com/maplecumt/blogImages/master/introduction-of-software-release-life-cycle/software-release-life-cycle.png)

从图中可以看到，软件的整个版本周期包括两个大的部分：开发测试阶段和发布阶段。

开发测试阶段有我们比较熟悉的alpha、beta，以及在此之前的pre-alpha和在此之后的release candidate，也就是前言里提到的RC版本。

在发布阶段，又有RTM、GA以及Production等版本阶段。

# 开发测试阶段

## Pre-alpha

有时候软件会在Alpha或Beta版本前先发布Pre-alpha版本。一般而言相对于Alpha或Beta版本，Pre-alpha版本是一个功能不完整的版本。

## Alpha (内部测试版)

Alpha版本仍然需要测试，其功能亦未完善，因为它是整个软件发布周期中的第一个阶段，所以它的名称是“Alpha”，希腊字母中的第一个字母“α”。这个版本一般不会对外发布。

Alpha版本通常会送到开发软件的组织或某群体中的软件测试者作内部测试。在市场上，越来越多公司会邀请外部客户或合作伙伴参与其测试。这令软件在此阶段有更大的可用性测试。

在测试的第一个阶段中，开发者通常会进行白盒测试。其他测试会在稍后时间由其他测试团体以黑盒或灰盒技术进行，不过有时会同时进行。

## Beta (外部测试版)

Beta取自希腊字母中的第二个字母“β”，表示软件测试阶段的第二个大的版本。

Beta版本是软件最早对外公开的软件版本，由公众参与测试。一般来说，Beta包含所有功能，但可能有一些已知问题和较轻微的BUG。Beta版本的测试者通常是软件开发组织的用户或者客户，他们会以免费或优惠价钱得到软件。Beta版本也被用作查看市场的反馈和用户的建议的一个版本。

其他情况，例如微软曾以Community Technology Preview（简称CTP，中文称为“社区技术预览”）为发布软件的测试版本之一，微软将这个阶段的软件散布给有需要先行试用的用户或厂商，并收集这些人的使用经验，以便作为进一步修正软件的参考。


## Release Candidate, RC

Release Candidate（简称RC）指可能成为最终产品的候选版本，如果未出现问题则可发布成为正式版本。在此阶段的产品通常包含所有功能、或接近完整，亦不会出现严重问题。

多数开源软件会推出两个RC版本，最后的RC2则成为正式版本。闭源软件较少公开使用，微软公司在Windows 7上应用此名称。苹果公司把在这阶段的产品称为“Golden Master Candidate”（简称GM Candidate），而最后的GM即成为正式版本。再比如，React 16就有两个RC版本，分别是Release 16.0.0-rc.1以及Release 16.0.0-rc.2。

当然，也有些软件厂商继续采用希腊字母来表示这一阶段的版本号，例如γ(gamma)，δ(delta)。


# 发布阶段

## Release to Manufacting, RTM

生产商发放（Release to Manufacturing，缩写RTM）是软件产品准备交付时使用的术语。某些计算机程序以“RTM”作为软件版本代号，例如微软Windows 7发行零售版前的RTM版本主要是发放给组装机生产商用，使制造商能够提早进行集成工作或解决软件与硬件设备可能遇到的错误。RTM版本并不一定意味着创作者解决了软件所有问题；仍有可能向公众发布前更新版本。以Windows 7为例：RTM版与零售版的版本号是一样的。

## General availability, GA

一般可用（General availability, 缩写GA）是所有必要的商业活动已经完成，该软件产品已经可以发售的阶段。然而，这取决于语言、地域和电子设备与媒体的可用性。商业活动可能也包括安全性和合法测试，以及本地化和全球销售的可能性评估。RTM与GA的间隔可能会是1周或几个月，因为在此过程中需要进行许多商业活动·。在这个阶段，可以说软件已经“上线”了。

## Release to Web, RTW

网络分发（Release to Web，缩写RTW），或称Web发布是一种利用互联网进行分发的软件交付方式。制造商在这种类型的发布中并不生产实体软件。随着互联网使用人数的增长，RTW变得越来越普遍。


# 参考文档

本篇文章大部分来自维基百科的内容。

- http://blog.csdn.net/linxinzheng/article/details/2201043
- https://en.wikipedia.org/wiki/Software_release_life_cycle
- https://baike.baidu.com/item/%E8%BD%AF%E4%BB%B6%E7%89%88%E6%9C%AC