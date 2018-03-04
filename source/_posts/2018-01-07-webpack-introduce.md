---
layout: post
section-type: post
title: 模块化和Webpack入门
tag: Webpack
category: Tech
date: 2018-01-07
---
![](https://raw.githubusercontent.com/maplecumt/blogImages/master/webpack-introduce/webpack.png)
<!-- more -->
# 简介

本质上，webpack 是一个现代 JavaScript 应用程序的模块打包器(module bundler)。当 webpack 处理应用程序时，它会递归地构建一个依赖关系图(dependency graph)，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 bundle。(摘自[webpack中文文档](https://doc.webpack-china.org/concepts/))




# 模块化
我们现在已经对前端的模块化习以为常了，但是，想想就在前几年，前端的模块化解决方案层出不穷。出现了各种规范和工具。所以，介绍webpack之前，先简述一下前端模块演进历史。

## CommonJS
CommonJS 是以在浏览器环境之外构建 JavaScript 生态系统为目标而产生的项目，比如在服务器和桌面环境中。

这个项目最开始是由 Mozilla 的工程师 Kevin Dangoor 在2009年1月创建的，当时的名字是 ServerJS。并于2009年8月改名为 CommonJS，以显示其 API 的更广泛实用性。

CommonJS 规范是为了解决 JavaScript 的作用域问题而定义的模块形式，可以使每个模块它自身的命名空间中执行。该规范的主要内容是，模块必须通过 module.exports 导出对外的变量或接口，通过 require() 来导入其他模块的输出到当前模块作用域中。

CommonJS就是为JS的表现来制定规范，因为js没有模块的功能所以CommonJS应运而生，它希望js可以在任何地方运行，不只是浏览器中。Node就是采用了CommonJS规范。

## AMD

AMD（Asynchronous Module Definition 异步模块定义）是为浏览器环境设计的，因为 CommonJS 模块系统是同步加载的，当前浏览器环境还没有准备好同步加载模块的条件。它采用异步方式加载模块，模块的加载不影响它后面语句的运行。所有依赖这个模块的语句，都定义在一个回调函数中，等到加载完成之后，这个回调函数才会运行。

AMD 定义了一套 JavaScript 模块依赖异步加载标准，来解决同步加载的问题。[中文文档](https://github.com/amdjs/amdjs-api/wiki/AMD-(%E4%B8%AD%E6%96%87%E7%89%88))

## CMD
AMD 是 [RequireJS](http://requirejs.org/) 在推广过程中对模块定义的规范化产出。[CMD(Common Module Definition)](https://github.com/seajs/seajs/issues/242) 是 [SeaJS](https://github.com/seajs/seajs) 在推广过程中对模块定义的规范化产出。是玉伯大大推出的专注于浏览器的js模块加载规范。
## UMD
Universal Module Definition，AMD和CommonJS的一种兼容性写法。同时支持两种风格，使AMD和CommonJS和谐相处。
## ES6模块
ES6 在语言标准的层面上，实现了模块功能，而且实现得相当简单，完全可以取代 CommonJS 和 AMD 规范，成为浏览器和服务器通用的模块解决方案。ES6 模块的设计思想，是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。

# 安装
webpack的安装非常简单，和普通的node应用一样`$ npm install webpack -g`即可安装。

# 配置

## 跑起来
简单的使用webpack还是很容易的。假如我们的文件结构是

|--index.html
|--js
    |--data.js
    |--index.js
|--dist/dist.js

index.js里只是简单的写一句对data.js的引用例如：

```javascript
var data = require("./data");
```
直接使用webpack命令行工具：

```
webpack js/index.js dist/dist.js
```

则我们可以在dist.js里看到打包后的代码，data.js也会根据引用关系打包进去。webpack的初次实践就完美的完成啦。

## webpack.config.js
webpack之所以强大，只是一个简单的命令行工具是完全不够的。所以我们要借助webpack.config.js的配置来完成更加复杂的打包任务。

首先，在根目录创建package.json文件，用来配置webpack相关依赖：
```json
{
    "name": "webpack-example",
    "version": "1.0.0",
    "description": "A simple webpack example.",
    "main": "bundle.js",
    "keywords": [
        "webpack"
    ],
    "author": "maple.yf",
    "license": "MIT",
    "dependencies": {
        "webpack": "^1.12.2"
    }
}

```

其次，创建webpack.config.js文件用来配置打包信息，比如文件入口、打包输出：

```javascript
var webpack = require('webpack')

module.exports = {
    entry: './js/index.js',
    output: {
        path: __dirname + '/dist',
        filename: 'dist.js'
    },
    module: {
        rules: []
    },
    plugins: [
        
    ]
}
```

完成配置之后，在命令行中输入webpack，就和上一节中输入的`webpack js/index.js dist/dist.js`是一样的效果。

## loader
loader 用于对模块的源代码进行转换。loader 可以使你在 import 或"加载"模块时预处理文件。因此，loader 类似于其他构建工具中“任务(task)”，并提供了处理前端构建步骤的强大方法。loader 可以将文件从不同的语言（如 TypeScript）转换为 JavaScript，或将内联图像转换为 data URL。loader 甚至允许你直接在 JavaScript 模块中 import CSS文件！

其实，loader就是帮助webpack处理非JavaScript文件。在webpack 1.x中，是通过module.loaders来配置的，升级到webpack 2.0后，loader配置项被功能更为强大的rules取代。[官方文档loader](https://doc.webpack-china.org/concepts/loaders)。


## plugins

插件被webpack官方描述为支柱性功能。它是用来解决loader无法完成的其他事情的。webpack自身提供一些插件，也有很多第三方插件可以使用。能够好好使用插件，将为我们的项目打包提供非常大的便利。将专门抽出一篇来讲解webpack插件的使用技巧。





# 参考资料
- https://doc.webpack-china.org/concepts/
- http://zhaoda.net/webpack-handbook/what-is-webpack.html
- https://div.io/topic/1752
- http://www.ruanyifeng.com/blog/2014/09/package-management.html
- https://webpack.js.org/comparison/