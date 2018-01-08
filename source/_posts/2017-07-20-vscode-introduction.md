---
layout: post
section-type: post
title: 前端编程利器VS Code
category: VS Code
tag: tech
---

## 前言

先来个icon镇楼 ^_^


![](https://raw.githubusercontent.com/maplecumt/blogImages/master/2017-07-12-vscode-introduction/icon.png)




前端同学使用的编辑器可选范围非常广泛。

最开始接触到前端的时候，听说了[Dreamweaver](http://www.adobe.com/cn/products/dreamweaver.html)这么一个强大的软件，但严格意义上讲，这不能算作一个编辑器。后来认识了NotePad++，在当时，这确实是一款非常好用的编辑器，语法高亮的友好度仅次于IDE，而且占用内存小，运行非常流畅。

再然后，有人推荐[Sublime](https://www.sublimetext.com/)。我用的时候，还是Sublime 2，最吸引我的是它的mini map，拖动mini map快速浏览大段大段的代码，比拖动小小的滑块酸爽很多呀。再加上后来安装的各种插件，感觉我进入了一个全新的世界，Sublime才是我最想用的编辑器呀！

工作之后，听说大家都在用[webstorm](https://www.jetbrains.com/webstorm/)，于是我也安装了一个试试，功能确实强大，特别它自带的git管理以及编辑器内部打开terminal的功能，非常适合前端开发。但是，功能强大的webstorm太过于笨重，每次打开的时候都要等一会儿，占用内存太高，同时开启两个项目的时候，电脑就会特别卡，非常影响写代码的心情，而且，webstorm是收费软件，用了一段时间之后果断放弃。

这时，我尝试了一款觊觎已久的酷炫编辑器 [Atom](https://atom.io/)。用了Atom之后，我才知道了什么叫酷炫！Sublime算什么，我再也不要用那个丑丑的Sublime了。基于[Electron](https://zh.wikipedia.org/wiki/Electron_(%E8%BD%AF%E4%BB%B6%E6%A1%86%E6%9E%B6))（最初以Atom Shell知名）和许可使用[Chromium](https://zh.wikipedia.org/wiki/Chromium)和Node.js的跨平台应用框架，并使用[CoffeeScript](https://zh.wikipedia.org/wiki/CoffeeScript)和[Less](https://zh.wikipedia.org/wiki/LESS_(%E5%B1%82%E5%8F%A0%E6%A0%B7%E5%BC%8F%E8%A1%A8))编写。Atom不但酷炫而且强大，因为有着活跃的社区，所以插件非常多，除了满足开发的刚需之外，还有很多想都想不到的插件。但是但是，美中不足的是Atom太卡了，而且用的时候偶尔还会崩溃。坚持用了一个月，最后实在受不了，我又换回Sublime了，但是心中很不甘啊！

当时我就想着，如果有一款编辑器可以像Sublime一样流程同时又像Atom一样酷炫该有多好。于是，我遇到了VS Code。VS Code刚刚发布Beta版时我尝试着用过一次，当时还不稳定，社区也不完善，插件更是贫乏，所以没留下好印象。这次重新尝试，是因为听说它和Atom一样，也是通过Electron编写的，我想，至少可以像Atom一样酷炫吧。试用之后才发现，原来这才是我一直苦苦寻找的理想编辑器呀！

## 特性

我强烈推荐VS Code的原因是它有以下几大特点：
- **酷炫** 和Atom一样采用Electron框架编写，整个软件其实就是一个WebAPP，样式深度定制，酷炫到超乎你想象。如果觉得还不过瘾，可以自己编写theme插件，满足你的各种癖好。
- **轻量** 虽然同样是采用Electron框架编写，但是VS Code和Atom走了不同的路线。Atom从一开始就把插件化架构摆在第一位，所以，Atom中最重要的是灵活而又完备的API，性能则不那么重要。VS Code则是把用户体验放在第一位，高性能、更能丰富才是它的首要目的，所以，一开始VS Code的插件系统很糟糕。但是VS Code的性能绝对高出Atom一个档位。
- **开源** 继承了Electron的良好基因。
- **跨平台** 依然是继承了Electron的良好基因。
- **丰富的插件** 虽然不如Sublime和Atom数量多，但现在已经有越来越多的插件涌入。
- **活跃的社区** 得益于Electron和Atom，VS Code的社区也是非常的活跃，更加快了插件生态的繁荣。

## 自带功能

### Emmet

VS Code不需要安装插件，自身就实现了Emmet，默认就是打开的。

### 智能感知

VS Code本身自带JS代码提示和自动补全功能，当然，如果你觉得不够用，还可以安装各种intelligence或者snippets插件来满足需求。

![JS智能提示](https://raw.githubusercontent.com/maplecumt/blogImages/master/2017-07-12-vscode-introduction/js-intelligence.png)

### Format Document

对于压缩的代码，或者格式不够规范的代码文件，可以通过这个命令一键格式化代码。当然，这个功能是每个编辑器应该都有的，并不是亮点。


![Fromat Document](https://raw.githubusercontent.com/maplecumt/blogImages/master/2017-07-12-vscode-introduction/format-document.png)

### Auto Save

自动保存功能也是大部分优秀的编辑器应该必备的。我认为VS Code里做的比较人性化的一个点是，它的设置选项里提供了四种自动保存的时机供我们选择：**off**、**afterDelay**、**onFocusChange**(编辑器失去焦点)、**onWindowChange**(窗口失去焦点)。如果设置为**afterDelay**，则可在 `files.autoSaveDelay` 中配置延迟。我比较喜欢**onWindowChange**。


![Auto Save](https://raw.githubusercontent.com/maplecumt/blogImages/master/2017-07-12-vscode-introduction/auto-save.png)


### Terminal

VS Code自带打开Terminal的功能，这是Atom和Sublime所不具备的。这也算是VS Code的一大亮点。

![Terminal](https://raw.githubusercontent.com/maplecumt/blogImages/master/2017-07-12-vscode-introduction/terminal.png)

## 插件推荐

接下来，推荐一些我用到过的非常实用的插件，帮助你编程时候事半功倍！

### [Git History](https://github.com/DonJayamanne/gitHistoryVSCode)

![Git History](https://raw.githubusercontent.com/maplecumt/blogImages/master/2017-07-12-vscode-introduction/git-history.gif)

可以查看一个文件的所有提交记录，同时还可以调出一个可视化的界面展示文件的提交记录，是git log的强化版。还可以查看某一行的所有提交记录。

### [Git Peoject Manager](https://github.com/felipecaputo/git-project-manager)

这是一个git项目管理的插件，一共就4个命令：
- **GPM: Open Git Project (Ctrl+Alt+P)**：打开git项目
- **GPM: Refresh Projects**：刷新git项目
- **GPM: Refresh specific project folder**：刷新特定路径下的git项目
- **GPM: Open Recent Git Project (Ctrl+Shift+Q)**：最近打开的git项目列表


![Git Project Manager](https://raw.githubusercontent.com/maplecumt/blogImages/master/2017-07-12-vscode-introduction/git-project-manager.gif)


插件的使用也很简单，找到配置文件中`gitProjectManager.baseProjectsFolders`把git项目的根目录放进去，就像下边这样：
`
{
    "gitProjectManager.baseProjectsFolders": [
        "/home/user/nodeProjects",
        "/home/user/personal/pocs"
    ]
}
`

然后`cmd + shift + P`调出命令栏，并输入`GPM`，上述的4个命令就被列出来了，选择`Refresh Projects`，稍等一会儿后，被我们添加到配置文件里的路径下的所有git项目都会被列出来。选择你的工作目录开始Coding吧！

### [Git Lens](https://github.com/eamodio/vscode-gitlens)

这是一款非常强大的git插件，它提供的每一个功能，都戳中了我们日常开发中的需求痛点。所以，我强烈推荐大家安装并使用这款插件。先目睹一下它的功能概览gif图：

![gitlens-preview.gif](http://upload-images.jianshu.io/upload_images/806919-0c09d650b1b21143.gif?imageMogr2/auto-orient/strip)

##### Code Lens

在文件的顶部展示代码变更的总的记录，包括左边的最新修改记录以及右边的所有的修改作者数量。

![Code Lens](https://raw.githubusercontent.com/maplecumt/blogImages/master/2017-07-12-vscode-introduction/git-lens.gif)

##### Blame Annotations

点击右边的作者数量可以进入整个文件的Blame Annotations。这里展示了每一行的最后一条修改记录，具体的展示方式可以在设置里自己配置，包括作者、时间和commit信息。

![Blame Annotations](https://raw.githubusercontent.com/maplecumt/blogImages/master/2017-07-12-vscode-introduction/blame-annotations.png)

##### Status Bar Blame

这个是指在状态栏里展示当前光标所在行的Git Blame信息。当然这里要展示的信息和格式也是可以配置的。这样，光标所在的行的最新git记录和作者信息完全展示在了状态栏里。

![Status Bar Blame](https://raw.githubusercontent.com/maplecumt/blogImages/master/2017-07-12-vscode-introduction/status-bar-blame.png)

##### Interactive Blame

这个功能和Status Bar Status类似，只不过，git信息是直接展示在文件中的代码后边。鼠标悬停在git记录上时，会有更详细的git变更气泡弹出。就像下边这样：

![Interactive Blame](https://raw.githubusercontent.com/maplecumt/blogImages/master/2017-07-12-vscode-introduction/interactive-blame.png)

##### Quick Menu

快捷键`shift + alt + H`调出**branch history quick pick menu**，  这个菜单功能非常强大，我们可以查看之前的commits信息、所有commits信息、根据message/author/filename搜索commits信息、查看一些文件的历史记录等。

![Quick Menu](https://raw.githubusercontent.com/maplecumt/blogImages/master/2017-07-12-vscode-introduction/quick-menu.png)

![Search by messages](https://raw.githubusercontent.com/maplecumt/blogImages/master/2017-07-12-vscode-introduction/search-by-messages.png)

![Search by autor 01](https://raw.githubusercontent.com/maplecumt/blogImages/master/2017-07-12-vscode-introduction/search-by-author01.png)

![Search by autor 02](https://raw.githubusercontent.com/maplecumt/blogImages/master/2017-07-12-vscode-introduction/search-by-author02.png)

![Search by filename 01](https://raw.githubusercontent.com/maplecumt/blogImages/master/2017-07-12-vscode-introduction/search-by-filename01.png)

![Search by filename 02](https://raw.githubusercontent.com/maplecumt/blogImages/master/2017-07-12-vscode-introduction/search-by-filename02.png)

通过message查找时，直接在输入框里输入message的关键信息即可。通过author查找时，则是输入`@author`，类似于图中的`@Zeke`。而通过filename查找，则需要注意一下，这里应该是`: filepath`，也就是相对于当前项目根目录的相对路径。类似于图中的`:lib/browser/chrome-extension.js`。除了这些之外，还可以根据commit id查找，这个用的不多，这里就不再举例了。

### [Project Manager](https://github.com/alefragnani/vscode-project-manager)

项目管理插件，这个功能和Git Project Manager有点类似，只不过，这个不但能管理git项目，还可以管理其他项目。


![Project Manager](https://raw.githubusercontent.com/maplecumt/blogImages/master/2017-07-12-vscode-introduction/project-manager-commands.png)


这个插件一共5个命令：
- **Project Manager: Edit Project Edit** 跳转到配置文件 projects.json 进行项目列表目录的配置修改。
- **Project Manager: List Projects** 列出已经保存的项目列表。
- **Project Manager: List Projects to Open in New Window** 列出已保存的项目列表并在新窗口打开选中的项目。
- **Project Manager: Refresh Projects** 刷新项目列表。
- **Project Manager: Save Project** 保存当前项目到项目列表。

### 其他插件

其他的一些插件就不做详细介绍了，这里列出我用过的感觉比较好的，大家自己到github上查阅吧。[vscode-icons](https://github.com/vscode-icons/vscode-icons)、[vscode-fileheader](https://github.com/zhaopengme/vscode-fileheader)、[Document This](https://github.com/joelday/vscode-docthis)、[CSS Peek](https://github.com/pranaygp/vscode-css-peek)、[File Peek](https://github.com/abierbaum/vscode-file-peek)、[Markdown PDF](https://github.com/yzane/vscode-markdown-pdf)、[Markdown Preview Enhanced](https://github.com/shd101wyy/vscode-markdown-preview-enhanced)、[Regex Railroad Diagrams](https://github.com/kogai/vscode-regex-railroad-diagrams)。

如果还有其他比较好用或者有意思的插件，欢迎大家前来留言。一起讨论交流。