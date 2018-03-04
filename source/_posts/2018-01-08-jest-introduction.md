---
layout: post
section-type: post
title: Jest自动化测试简介
category: Tech
tag: Auto Test
date: 2018-01-08
---
![](https://raw.githubusercontent.com/maplecumt/blogImages/master/jest/jest.png)
<!-- more -->
# 简介

Jest 被 Facebook 用来测试包括 React 应用在内的所有 JavaScript 代码。Jest 的一个理念是提供一套完整集成的 “零配置” 测试体验。
# 基础测试
通过test和expect函数来完成一次最简单的测试：

```javascript
const sum = require('./sum');

test('adds 1 + 2 to equal 3', () => {
    expect(sum(1, 2)).toBe(3);
});
```
如果sum函数返回的值就行我们测试描述的那样是3的话，测试通过。

# 结合enzyme
enzyme是aribnb开源的一套测试React的库。它提供的mount方法可以模拟React里的render生成对应的DOM字符串，另外还提供了类似simulate的方法用来模拟事件操作。比如下边的测试例子：
```jsx
it("should provide the actions and subscribe to changes", () => {
    store.setState({ count: 0 })
    const Comp = ({ count, increment }) => (
        <h1 onClick={increment}>{count}</h1>
    )
    const mapToProps = ({ count }) => ({ count })
    const actions = store => ({
        increment: state => ({ count: state.count + 1 })
    })
    const ConnectedComp = connect(mapToProps, actions)(Comp)
    const App = () => (
        <Provider store={store}>
            <ConnectedComp />
        </Provider>
    )
    const wrapper = mount(<App />)
    expect(wrapper.html()).toBe("<h1>0</h1>")
    wrapper.children().simulate("click")
    wrapper.children().simulate("click")
    expect(wrapper.html()).toBe("<h1>2</h1>")
})
```
使用mount方法模拟render，通过html方法把DOM结构转换成字符串，通过simulate来模拟单击事件。从而完成整个测试用例。
# 快照测试
enzyme里提供的方法都是基于React的，但是对于类React库而言，这些并不能使用比如Rax。不过，Jest提供了一种快照测试，可以通过快照的方式这是render后的DOM结构。

快照测试是通过记录React结构树快照或其他可序列化的值，来简化 Ui 测试，并分析state如何随时间变化而改变。

一个典型的快照测试案例是，为移动端应用的UI组件截个图，和需要测试参考图进行比较。如果两张图片不一致，说明测试不通过：可能是非法修改造成的，也可能是UI组件未及时render造成的。

## Jest Snapshot
在测试react组件时，也可以采用相同的思路进行快照测试。只不过，我们不是通过截图对比，而是保存render时所生成的序列化React tree。例如：

```javascript
import React from 'react';
import Link from '../Link.react';
import renderer from 'react-test-renderer';

it('renders correctly', () => {
    const tree = renderer
        .create(<Link page="http://www.facebook.com">Facebook</Link>)
        .toJSON();
    expect(tree).toMatchSnapshot();
});
```

## 生成 snapshot file

第一次运行该测试脚本时，Jest会自动生成一个 snapshot file，路径默认是 `./__snapshot__`。文件内容如下所示：

```javascript
exports[`renders correctly 1`] = `
<a
    className="normal"
    href="http://www.facebook.com"
    onMouseEnter={[Function]}
    onMouseLeave={[Function]}
>
    Facebook
</a>
`;

```
之后再次运行测试脚本的时候，Jest会自动比对render输出的结果和之前的snapshot file的差异，如果相同，则测试通过。

## 更新 snapshot file
由于每次运行结果都会和第一次的 snapshot file 进行比对，如果我想更换比对的 snapshot file文件内容，应该怎么办呢？


首先，假如我们有如下场景，更换前面的Link组件的链接，代码如下：

```javascript
import React from 'react';
import Link from '../Link.react';
import renderer from 'react-test-renderer';

it('renders correctly', () => {
    const tree = renderer
        .create(<Link page="http://www.instagram.com">Facebook</Link>)
        .toJSON();
    expect(tree).toMatchSnapshot();
});
```

这时，运行测试脚本时，测试失败。因为render出的快照结果和本次存储的初次 snapshot file内容不一致。此时，如果我想把本次的render结果作为 snapshot file的内容供以后测试比对，可以运行一下命令进行更新：

```
jest --updateSnapshot
```

## rax-test-renderer

针对Rax测试，官方提供了一个对应的npm包，[rax-test-renderer](https://github.com/alibaba/rax/tree/master/packages/rax-test-renderer)。

利用它提供的renderer替换react的renderer就可以对rax进行快照测试了。


# 异步测试
使用Jest进行异步测试，有以下三种方式。
## assertions
通过断言的方式进行测试，所调用的异步方法必须返回一个promise对象。

```javascript
it('works with promises', () => {
    expect.assertions(1);
    return user.getUserName(4).then(data => expect(data).toEqual('Mark'));
});
```

## async/await
使用这种方式，更显得简单一些，可以和之前的同步测试一样的思路写测试用例。只不过，在异步方法前边加上await关键字用来表示异步执行。

```javascript
it('works with async/await', async () => {
    expect.assertions(1);
    const data = await user.getUserName(4);
    expect(data).toEqual('Mark');
});
```

## done
done是异步测试的一种弥补方式，如果需要测试的异步方法没办法返回promise或者不方便转换成async/await的写法，可以通过done方法来实现这种场景的异步测试。

```javascript
test('the data is peanut butter', done => {
    function callback(data) {
        expect(data).toBe('peanut butter');
        done();
    }
    fetchData(callback);
});
```
例如上边的例子，callback是一个异步调用，正常的测试流程下，是不会等着回调再进行测试的。所以Jest加入done方法，done方法被调用的时候，整条测试才会完成。如果done一直没有调用，则测试失败。
# API
Jest提供了非常丰富的测试API，一共分为以下几类。
## Globals
全局API：在测试工程中，这些方法或对象直接放到了全局环境中，不需要额外的引入。其中比较常用的有afterAll(fn, timeout)、afterEach(fn, timeout)、beforeAll(fn, timeout)、beforeEach(fn, timeout)，分别表示所有测试结束时调用，每个测试结束时调用，所有测试开始前调用，每个测试开始前调用。

## Expect
这是Jest的关键API，通过expect对象提供的方法，我们用来描述期望得到的结果。expect.toBe() expect.toEqual() expect.toMatch() expect.toMatchObject()等。

## Mock Functions
用来测试函数的间接调用过程，并把调用过程中的返回信息存储下来。比如测试forEach的调用过程，为传入的数组中的每个元素调用一个回调函数。
```javascript
//通过jest.fn()创建供forEach调用的回调函数
const mockCallback = jest.fn();
forEach([0, 1], mockCallback);

// 此模拟函数被调用了两次
//mockCallback.mock.calls中记录了每次调用的结果
expect(mockCallback.mock.calls.length).toBe(2);

// 第一次调用函数时的第一个参数是 0
expect(mockCallback.mock.calls[0][0]).toBe(0);

// 第二次调用函数时的第一个参数是 1
expect(mockCallback.mock.calls[1][0]).toBe(1);
```
## The Jest Object
jest是一个全局对象，在测试文件中可以直接调用。比如上边的例子中的jest.fn()。jest对象里提供了一些系统方法，可以工号的控制整个测试行为和流程。
## Configuring Jest
Jest的配置可以直接在package.json中进行设置。

```json
"jest": {
    "verbose": true,/*展示详细的测试结果*/
    "moduleFileExtensions": [ "jsx", "js" ], 
    "setupFiles": [
        "<rootDir>/config/testSetup.js" /*配置入口文件*/
    ],
    "transformIgnorePatterns": [
        "node_modules/(?!(FOXRax)/)" /*不忽略node_modules中指定模块的ES6转换(默认情况下，transform转换不作用于node_modules中的模块)*/
    ],
    "transform": {
        "^.+\\.(js|jsx)$": "babel-jest" /*js、jsx指定babel转换*/
    },
    "testMatch": [
        "<rootDir>/src/**/*.spec.(js|jsx)" /*测试文件匹配*/
    ]
},

```
## Jest CLI Options
Jest命令行工具也提供了一些实用的选项。当然，命令行选项也可以在配置文件里设置。比如比较实用的 `--json --outputFile=<filename>` 的配合使用就可以以json的格式把测试结果输出到本地文件中。
# 参考文献

- http://facebook.github.io/jest/docs/en/snapshot-testing.html#snapshot-testing-with-jest
- https://facebook.github.io/jest/docs/en/api.html