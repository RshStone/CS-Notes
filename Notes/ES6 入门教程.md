# ECMAScript 6

https://es6.ruanyifeng.com/#docs/let#let-%E5%91%BD%E4%BB%A4

## ECMAScript 6 简介

时间：2015年6月

是什么: 是JS语言的下一代标准.  

怎么做

为什么 目标：是使得 JavaScript 语言可以用来编写复杂的大型应用程序，成为企业级开发语言。

### 和JS的关系

类比：相对论和原子弹的关系

### 和ECMAScript 2015 的关系(了解历史)

直到今天，**初学者一开始学习 JavaScript，其实就是在学 3.0 版的语法。**

一种新的语法从提案到变成正式标准，需要经历五个阶段。每个阶段的变动都需要由 TC39 委员会批准。

- Stage 0 - Strawman（展示阶段）
- Stage 1 - Proposal（征求意见阶段）
- Stage 2 - Draft（草案阶段）
- Stage 3 - Candidate（候选人阶段）
- Stage 4 - Finished（定案阶段）

2009 年 12 月，ECMAScript 5.0 版正式发布。Harmony 项目则一分为二，一些较为可行的设想定名为 JavaScript.next 继续开发，后来演变成 ECMAScript 6；一些不是很成熟的设想，则被视为 JavaScript.next.next，在更远的将来再考虑推出。

**Babel转码器**

[Babel](https://babeljs.io/) 是一个广泛使用的 ES6 转码器，可以将 ES6 代码转为 ES5 代码

怎么用：

https://es6.ruanyifeng.com/#docs/intro

https://babeljs.io/

```js
// 转码前
input.map(item => item + 1);

// 转码后
input.map(function (item) {
  return item + 1;
});
```



### 和Node.js一些联系

Node.js 是 JavaScript 的服务器运行环境（runtime）。它对 ES6 的支持度更高。除了那些默认打开的功能，还有一些语法功能已经实现了，但是默认没有打开。使用下面的命令，可以查看 Node.js 默认没有打开的 ES6 实验性语法。

## let 和 const 命令

ES6 新增了`let`命令，用来声明变量。它的用法类似于`var`，但是所声明的变量，只在`let`命令所在的代码块内有效。 



















