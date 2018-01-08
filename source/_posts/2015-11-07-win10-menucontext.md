---
layout: post
title:  "win10右键反应缓慢"
date:   2015-11-07 11:00:00
section-type: post
tag: Windows
category: tech
---
最近装了win10，但是有一个小问题，右击电脑空白处想刷新的时候，反应特别慢，因为系统是安装在固态硬盘上的，所以不应该出现这种问题，于是网上搜罗了一些解决方法。
# 解决方案 #
开始，运行：regedit，打开注册表

```
    HKEY_CLASSES_ROOT/Directory/Background/shellex/ContextMenuHandlers
```

删除下面两个选项就可以了：一个是 igfxcui ,另外一个是NvCplDesktopContext如果只有一项就单独删除，如果两项都有就全部删除。