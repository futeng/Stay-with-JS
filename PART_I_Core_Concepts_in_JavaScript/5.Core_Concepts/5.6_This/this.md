- 说明顺序
  - 别人家的`this` 
    - `this` 关键字的历史
    - 各个语言对关键字 `this` 的实现
  - JS 家的 `this` 
    - JS 中 `this` 的历史
    - 为什么JS中要使用 `this`
      - 函数方面讲述：更简单且易于复用的API设计可能
      - 对象、原型方面：你就能理解函数可以自动引用上下文程序是多么的重要
  - 前置知识
    - 作用域知识、JS词法作用域知识
  - 初窥 this
    - 调用栈和执行上下文
    - 经典的 this 使用
    - 给 this 下定义
  - 对 this 的两个重大误解
    - 指向自身
    - this使用的作用域
  - 全面解析 this
    - 绑定规则
    - 优先级
    - 绑定例外
    - this 词法
  - 函数与this
  - 对象与this
  - 原型与this
- this 知识点来源
  - You don't know js - this 
    - 栈调用顺序
    - this 不使用词法作用域，是编译器隐形获取调用位置上下文的指示
    - this 的4种定义的方法和顺序
  - [bind and this - Object Creation in JavaScript P1 - FunFunFunction #43](https://www.youtube.com/watch?v=GhbhD1HR5vk)
    - 举例子说明了 bind、call、还有个函数之间的关系
  - [Javascript Context Tutorial - What makes Javascript Weird...and Awesome Pt5](https://www.youtube.com/watch?v=fjJoX9F_F5g&index=5&list=PLoYCgNOIyGABI011EYc-avPOsk1YsMUe_)
    - 说明了其实this 指示的是 context 上下文的含义
  - 加上国内的一些有些博客说明，对每个例子做详尽的解释即可



## 对 this 的两个重大误解

### 指向自身

- 误解：认为 this 是一个变量且始终指向（引用）函数自身
- 思路
  - 举例证明：this 并非是函数自带的隐式变量，this 并不属于函数本身
  - 尝试使用词法作用域知识来规避 this 的问题，但点明着同时也规避了对 this 的了解
  - 尝试强制指定this执行的上下文来实现状态的改变

```js
// 定义函数累加函数自身的变量 count
function foo() {
	this.count ++;
	console.log(this.count);
}
foo.count = 0;

foo(); //NaN
```

`foo.count` 定义了函数对象foo的一个属性 `count`，但实际执行foo函数，发现 `this.count` 却不是刚刚定义的函数对象内属性（返回了NaN）。

> 实际上当在 Global 作用域（浏览器里的全局对象是 window）里调用了foo函数，foo内部的this指向的是 Global 上下文。
>
> 我们理解为：为了让函数自己自发主动的寻找自己需要的数据，需要有个隐式的寻找机制。这个机制就是告诉函数，你应该在哪里寻找数据。而this就是指向了这个位置（上下文 Context）。
>
> 以上不必现在就理解，但请多读几遍，在脑海留下印象。

上述示例中对函数状态的处理，因为对this机制的不理解，通常会使用词法作用域来规避和解决问题。

```js
// 函数会向外层寻找同名变量：使用的是词法作用域的机制
function foo() {
	data.count++;
	console.log(data.count);
}

var data = {
	count:0
}
foo();// 1

// bar.count 使用 bar作为标识符的引用，还是使用了词法作用域机制
function bar() {
	bar.count++;
	console.log(bar.count);
}
bar.count = 0;
bar();
VM1009:3 1
```

此类问题常见的解决方案是使用 call/bind 等函数来强制更更改 this 引用的上下文。

```js
// 回到第一个例子，在调用的时候稍作修改
function foo() {
	this.count++;
	console.log(this.count);
}

foo.count = 0;
// foo函数调用的时候，通过call函数强制更改下this引用的上下文(更改到foo内)
foo.call(foo);
```

以上是为了说明 this 从来都不是像一个变量一样，指向函数本身，this 指向的是一个位置。

首先你得明白，在『分工的智慧』章节描述的，其实是为了提升函数主动解决问题的能力，制定了一个机制，即：使用this去指向函数应该从哪里获取数据的位置（Context）。