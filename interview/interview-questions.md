## 前言

大家好，我是chenzilin。众所周知，面试是我们通往其他更高平台的必经之路之一，前段时间刚好在查漏补缺，经过1个多月的爆肝，我整理了一份前端史上最全的面试题（附答案）！本面试题面向所有前端“攻城狮”，希望这份面试题能给各位看官查漏补缺，帮助各位看官通往更高的平台。

这份面试题会**持续更新优化**，如果大佬们有好的题目或答案，可以通过评论区或【Issues】的方式告诉我，我将进行同步更新~

每个栏目分为**Easy**（简单）、**Medium**（中等）、**Hard**（困难）三种难度任供各位看官选择。

如果文中有任何错误，欢迎👏🏻大佬们在评论区指正，也可以通过【Issues】的方式，我会定期进行修改~

由于时间关系，

以下是整体的目录结构

```
├── HTML
├── CSS
├── JavaScript
├── TypeScript
├── Node
├── 浏览器
├── MVVM框架
│   ├── Vue
│   ├── React
├── 前端工程化
├── 前端优化
├── 前端监控
├── 前端安全
├── 跨端开发
│   ├── 微信小程序
│   ├── React Native
│   ├── Flutter
├── 计算机基础
├── 计算机网络
├── 数据结构和算法
├── 设计模式
├── 测试
├── 手写函数
```

**码字不义，你的点赞、评论、收藏、关注，都将成为我创作的动力！！！**

> 未经允许，请勿转载，谢谢。




## HTML

### ⭐️Easy

#### 1. DOCTYPE有什么用？

DOCTYPE是一种标准通用标记语言的文档类型声明，目的是告诉标准通用标记语言解析器要使用什么样的文档类型定义（DTD）来解析文档。

#### 2. img标签的title和alt属性有什么区别

title表示鼠标放到图像上时显示的文案，alt表示图片失效时显示的替代文案。

####  3. 简述一下src与href的区别

href用于建立页面与外部资源的关系，不会阻塞dom解析，src用于替代这个元素，会阻塞dom解析。

#### 4. H5和H4有什么不同？

H5引入原生多媒体支持，引入canvas，引入语义化标签，新增离线存储等等。



### ⭐️⭐️Medium

#### 1. SVG和CANVAS的区别？

从三个角度分析

图像：svg是矢量图，基于xml，放大不失真，canvas是位图，使用js绘制，放大会失真。

事件：svg支持事件处理器，canvas不支持事件处理器。

适合领域：svg适合图像，canvas适合游戏。

#### 2. script标签中defer 和 async 的区别 ?

defer和async都会进行异步加载脚本，defer在dom解析完之后执行，async下载完立马执行。

#### 3. style标签prefetch和preload区别？

prefetch和preload都会提前加载资源，但prefetch什么时候加载由浏览器决定。

### ⭐️⭐️⭐️Hard

✍️待补充



<hr />

## CSS

### ⭐️Easy

#### 1. CSS 属性是否区分大小写？

不区分大小写。

#### 2. CSS的盒模型？

CSS盒模型分为标准盒模型和替代（IE）盒模型，标准盒模型通过`box-sizing: content-box`设置，实际宽度=width+border+padding，替代盒模型通过`box-sizing: border-box`设置，实际宽度=width。

#### 3. link与@import的区别？

从四个角度分析

从属关系：link不仅可以加载样式表，还可以加载比如font等其他资源，@import只能导入样式表。

兼容性：link兼容性比@import好。

加载顺序：link加载页面时加载，@import在页面加载完毕之后再加载。

可控性：link支持js动态插入，@import不支持动态插入。

#### 4. CSS 选择器的优先级是如何计算的？

!important > inline style >  id > class > 元素 >  * > 继承

#### 5.讲讲margin塌陷？

✍️待补充



### ⭐️⭐️Medium

#### 1. 请阐述块格式化上下文（Block Formatting Context）及其工作原理

块级格式化上下文（BFC）是Web页面的可视化CSS渲染的部分，是块级盒布局发生的区域，也是浮动元素与其他元素交互的区域。

形成BFC的条件：根元素、float不为none、postions不为static和relative、overflow不为visible、弹性元素、栅格元素、多列容器。

解决了什么问题：margin塌陷、清除浮动、阻止元素被浮动元素覆盖。

#### 2. 请阐述z-index属性，并说明如何形成层叠上下文（stacking context）

z-index影响层叠上下文元素的层叠性，越大越靠上层，默认为auto。

层叠上下文是对html元素的一个三维构想，每个层叠上下文都独立于它的兄弟元素，当处理层叠时只考虑子元素，每个层叠上下文都是自包含的，当一个元素的内容发生层叠时，该元素将作为整体在父级层叠上下文中按顺序进行层叠。

解决什么问题：层叠上下文解决多个元素重叠时的优先级显示。

如何形成层叠上下文：根元素，position为absolute或relative且z-index不为auto，position为fixed或sticky，flex容器的子元素且z-index不为auto，grid容器的子元素且z-index不为auto，opacity小于1，transform、filter、prespective、clip-path、mask不为none，solation为isolate。

#### 3. CSS 有哪些继承属性

文本属性，字体属性，visibility。

#### 4. 有哪些清除浮动的技术？

1.`clear: both`

2.`overflow: auto/hidden`

3.

```css
.clearfix::after {
  content: '';
  display: block;
  clear: both;
}
```

#### 5. 响应式布局有哪些

媒体查询、百分比布局、rem、vw布局。



### ⭐️⭐️⭐️Hard

✍️待补充




<hr />

## JavaScript

### ⭐️Easy

#### 1. 什么是闭包？

闭包是一个函数有权访问另外一个函数作用域变量，通过闭包可以访问创建闭包时所处环境中的全部变量。闭包为函数创建时所处的作用域中的函数和变量创建“安全气泡”。通过这种方式，即使创建函数时所处的作用域已经消失，但是函数仍然能够获得执行时所需的全部内容。

##### 2. let const var比较

从4个方面来分析。

暂时性死区：var不支持暂时性死区，let和const有暂时性死区；

块级作用域：var不支持块级作用域，let和const支持块级作用域；

重复声明：var支持重复 声明，let和const不支持重复声明；

声明后修改值：var和let支持修改值，const不支持修改值。

#### 3. offsetWidth/offsetHeight,clientWidth/clientHeight 与 scrollWidth/scrollHeight 的区别

offset表示可视区+滚动条的宽高度，client表示可视区的宽高度，scroll表示实际的宽高度。

#### 4. mouseover/mouseout 与 mouseenter/mouseleave 的区别与联系

mouseover/mouseout/mouseenter/mouseleavet当鼠标移入移出元素时都会触发，mouseover/mouseout移入移出子元素也会触发。

#### 5. isNaN与Number.isNaN的区别

isNaN会尝试将参数转为数值，然后才会对转换的结果进行判断；Number.isNaN直接判断值是否为NaN，并且检查其类型是否为Number。

#### 6. 类数组和数组的区别，dom 的类数组如何转换成数组

类数组没有数组Array的方法，比如push、forEach等等。

类数组转数组的方法：

- `[...cArr]`
- `Array.prototype.slice.call(cArr)`
- `Array.from(cArr)`

#### 7. DOM事件机制，怎么阻止事件捕获

调用事件对象`event.stopImmediatePropagation`。



### ⭐️⭐️Medium

#### 1. js有哪些内置对象？

基本对象分为一般对象、函数对象和错误对象：

- 一般对象：Object、Boolean、Symbol
- 函数对象：Function
- 错误对象：Error、ReferenceError、TypeError、SyntaxError等等

字符串对象：String、RegExp；

值对象：Infinity、NaN、undefined；

数字和日期对象：Number、Date、Bigint、Math等等。

#### 2. 如何理解作用域、作用域链和执行上下文？

理解作用域，首先需要理解执行上下文，执行上下文分为全局执行上下文和函数执行上下文，当程序运行时，会创建一个全局执行上下文，当执行函数时，会创建一个函数执行上下文，当退出函数时，执行上下文也随着销毁。

当创建执行上下文时，会创建与之对应的作用域，作用域包含上下文中定义的标识符的映射表。作用域分别全局作用域、函数作用域和块级作用域。

当当前作用域访问不到变量时，会向外面的作用域访问，作用域的顶端是全局作用域，如果找到立即返回，如果顺着作用域链未找到该变量的引用，则抛出ReferenceError异常。

#### 3. 如何创建一个没有 prototype(原型)的对象？

`Object.create(null)`。

#### 4. 说说对原型链的理解

每个实例对象都有一个私有属性`__proto__`，指向构造函数的原型对象prototype，原型对象也有自己的原型`__proto__`，层层向上直到一个对象的原型`__proto__`为null。几乎所有的js对象都是Object构造函数的实例。

#### 5. JSON.stringify有什么缺点？

undefined、function和symbol在数组对象中会被忽略，单独转换会返回undefined。

循环引用对象会抛出错误。

以symbol为属性键的都会被忽略掉。

Date会调用toJSON()将其转换为string字符串。

NaN和Infinity及null会被当做null。

Map/St/WeakMap/WeakSet仅会序列化可枚举的属性。

#### 6. for...in 和 for...of的区别?

`for...in`以任意顺序迭代一个对象的除Symbol以外的可枚举属性，包括继承的可枚举属性。

`for...of`遍历可迭代对象定义要迭代的数据。

#### 7. new操作符都做了什么

创建一个对象，将对象的原型`__proto__`指向构造函数的原型对象`prototype`，将对象绑定到this并调用构造函数，如果构造函数返回对象或函数则直接返回，否则返回改对象。

#### 8. 介绍下 Promise 的特性、优缺点

Promise拥有3个状态，pending进行中、fulfilled已完成和rejected已拒绝，默认是pending，状态一旦改变不可变更，Promise对象接受一个回调函数，接受两个参数，resolve和reject，resolve调用将状态变成fulfilled，reject调用将状态变成rejected，在回调函数抛出错误，也会将状态变更为rejected。

Promise实例有3个方法，then方法接受两个回调函数，onFulfilled和onRejected，顾名思义，onFulfilled在Promise状态为fulfilled时触发，onRejected在rejected状态时触发；catch方法传入一个回调函数onRejected，rejected状态时触发。finally方法传入的回调函数，不管是fulfilled还是rejected都会触发。then、catch和finally方法的返回值是一个Promise实例，可以通过链式调用的方式继续调用。

Promise的优点是解决了回调地狱的问题，缺点第一是一旦新建就会立即执行，无法取消，第二是如果不设置回调函数，Promise内部抛出的错误不会反应到外部，除非手动监听rejectionhandled事件。

#### 9. 说一下事件循环机制Event Loop

事件循环负责处理异步任务，异步任务分为**macro task宏任务**和**micro task微任务**，分别对应宏任务队列和微任务队列，每次事件循环，会先处理一个宏任务和所有的微任务，同一时刻只执行一个任务，依次执行。

宏任务代表一个个离散的、独立工作单元，如执行JS主线程、解析HTML、更改当前URL以及各种事件，如页面加载、输入、网络事件和定时器事件等等。微任务是更小的任务，如Promise、DOM发生变化等等。微任务需要尽可能快的，通过异步的方式执行，同时不能产生新的微任务。微任务使得我们能够在重新渲染UI之前执行指定的行为，避免不必要的重绘。

一次事件循环会处理宏任务队列中的一个任务和微任务队列中所有的微任务。

<img src='https://images-1256612942.cos.ap-guangzhou.myqcloud.com/55ABVA.jpg' style="width: 50%">

#### 10. esmodule和commonjs的区别

从5个角度分析

加载：esm静态加载，代码发生在编译时；cjs支持动态加载，代码发生在运行时。

导出值：esm导出值是映射关系，可读，不可修改，但可通过导出的函数修改导出的值；cjs导出值的拷贝，可以修改导出的值。

文件后缀名：esm的文件后缀名是mjs；cjs的后缀名是cjs。

执行方式：esm提前加载并执行模块文件，在严格模式下执行，支持异步导入；cjs遇到require()会同步阻塞，直到新模块加载完成。

export导出使用：esm的export和export default支持一起使用；cjs的module.exports和exports不支持一起使用，会被覆盖。

#### 11. 解释下栈内存和堆内存？

栈内存比堆内存速度更快，堆内存比栈内存更存储更多的容量。

基本类型存储在栈内存，引用类型指针存储在栈内存，值存储在堆内存。

#### 12. 箭头函数与普通函数区别

从5个角度分析

this：箭头函数this默认指向外层执行环境的this。

arguments：箭头函数不绑定arguments。

new操作符：箭头函数不能用作构造函数。

prototype：箭头函数没有原型对象prototype。

yield关键字：yield不能在箭头函数中使用。

#### 13. 如何理解回流和重绘

当DOM的变化影响了元素的几何属性，浏览器需要重新计算元素的几何属性，同时其他元素的几何属性和位置也会因此受到影响，浏览器会使渲染树中受到影响的部分失效，并重新构造渲染树，这个过程称为回流（重排）。

触发回流的操作：页面首次渲染、浏览器窗口大小改变、元素尺寸或位置发生改变、元素内容变化、元素字体大小变化、添加或删除可见DOM元素、强制刷新队列（offset、scroll、client、getComputedStyle()、getBoundingClientRect()、scrollTo()）。

如何减少回流：使用cssText合并多次样式修改、批量修改DOM、使用虚拟DOM、避免频繁读取会引发队列刷新的属性、对具有复杂动画的元素使用绝对定位脱离文档流。

发生重排（回流）后，浏览器会重新绘制受影响的元素到屏幕中，这个过程称为重绘。

触发重绘的操作：修改元素的color、background-color、visibility等等。

回流一定会触发重绘，回流代价比重绘高。

#### 14. 讲讲this

this受函数调用方式的影响，函数有5中调用方式

作为普通函数调用，this指向window，严格模式为undefined。

作为构造函数调用，this指向实例对象。

作为方法，this指向关联的对象。

作为箭头函数调用，this指向外层上下文的this。

作为bind、call和apply调用，this指向传入的对象。

#### 15. WeakMap相比Map的优缺点是什么？

WeakMap和Map都是用于保存键值对。

WeakMap的键是弱引用，键必须是对象。

WeakMap的出现是为了解决Map中存在的查找、存储性能和内存泄漏问题。

缺点：WeakMap不支持遍历属性，如果需要遍历应使用Map。

### ⭐️⭐️⭐️Hard

#### 1. 说下JS垃圾回收与V8垃圾回收的区别

**JS垃圾回收**分为**引用计数**和**标记清除**：

引用计数是最初级的GC（Grabage Collection）算法，引用计数的原理是如果对象没有其他对象引用到它，对象将被GC，这里的引用指的是一个对象引用另一个对象，这里的对象不仅指js对象，还包括函数作用域和全局作用域。引用计数的缺点是循环引用，如果一个对象引用了自己，那么它将无法被GC。

标记清除的原理是从根部（全局作用域）出发，区分能到达的对象和不能到达的对象，之后将不能到达的对象进行GC。标记清除解决了循环引用的问题。

**V8垃圾回收**基于**分代式**垃圾回收机制，在V8中，所有js对象都是通过**堆**来进行分配，根据对象存活时间将内存分为**新生代**和**老生代**：

**新生代**存放的是存活时间较短的对象，比如一个局部作用域中的变量，新生代的内存在32位分配16M内存空间，64位中分配32M内存空间，算法采用的是**Scavenge算法**；Scavenge算法的原理：

1. 将堆内存分为两个semispace空间，一个处于使用状态（From空间），一个处于闲置状态（To空间），分配对象在From空间进行；
2. 开始进行GC时，会检查From空间的存货对象，将存活对象复制到To空间；
3. 将From空间释放，GC完成；
4. From和To空间名称互换；
5. 重复第一步的操作。

在下一次GC时，如果之前的对象还在新生代中，会进行晋升，晋升是将较长生命周期的对象移动到老生代中的一种操作，触发晋升的条件是：

- 一轮GC之后还存活的新生代对象
- 在拷贝过程中，To空间的使用率超过25%

新生代只能使用堆内存空间的一半，采用的是空间换取时间。

**老生代**存放的是存活时间较长或常驻内存的对象，比如全局对象、闭包等等，老生代32位分配700M内存空间，64位分配1.4G内存空间，老生代的GC算法是**Mark-Sweep标记清除**和**Mark-Compack标记整理**算法：

- Mark-Sweep标记清除：遍历堆中所有对象并标记活着的对象，在清除阶段清除没有被标记的对象，缺点是空间碎片化，分配大对象会触发没必要的GC。
- Mark-Compact标记整理：由Mark-Sweep标记清楚演变而来，区别是将活着的对象往一端移动，之后再进行清除。

说完两个GC算法，这里有个概念需要补充下，由于JS引擎是单线程，垃圾回收和代码执行过程都需要用到JS引擎，而垃圾回收执行优先级比代码执行要高，所以会造成代码暂停执行，等垃圾回收完毕之后再执行JS代码，这个过程称为**全停顿**，全停顿会造成页面卡顿现象，为了解决这个问题，V8采用了**Incremental Marking增量标记**算法，这个算法的原理是：

将一整段的垃圾回收操作拆分成多个小段来执行，垃圾回收与应用逻辑交替执行直到标记阶段完成，这个算法的优点是提高了执行效率。



<hr />

## TypeScript

### ⭐️Easy

#### 1. type和interface的区别

type右边可以是任意类型，interface右边必须为结构；interface支持声明合并，同一作用域多个同名interface将自动合并。

#### 2. 说说枚举的用法

枚举允许开发者定义一组常数，当一个变量有几种可能的取值时，可以将其定义为枚举类型，枚举支持数值和字符串，数值枚举默认从0开始递增，也可以手动设置数值，从该数值开始递增。

### ⭐️⭐️Medium

✍️待补充

### ⭐️⭐️⭐️Hard

✍️待补充

<hr />

## Node

### ⭐️Easy

✍️待补充

### ⭐️⭐️Medium

#### require一个模块时的查找过程

当`require`一个模块时，首先会先判断缓存中是否有该模块，有则直接返回，没有则进入查找阶段。`require`可分为3种类型：

- 作为文件模块

  如果模块是核心模块（比如fs、http等），直接返回；如果是绝对路径`/`开头，则从根目录开始查找；如果是相对路径`./`开头，则从当前`require`文件相对位置查找；如果文件名没有拓展名，则自动依次添加`.js`、`.json`、`.node`查找。

- 作为目录

  根据目录的package.json的main属性查找，如果没有则依次查找`index.js`、`index.node`。

- 作为第三方模块

  从当前目录的`node_modules`查找，如果当前目录的`node_modules`查找不到，则移动到父目录的`node_modules`查找直到根目录；如果设置了`NODE_PATH`环境变量，当上述查找不到时，会从`NODE_PATH`环境变量中的目录进行查找。

#### 如何理解中间件

中间件（Middleware）是为应用提供通用服务和功能的软件。数据管理、应用服务、消息传递、身份验证和API管理通常都要通过中间件。

在Node.js中，中间件主要是指封装http请求细节处理的方法，中间件的原理类似于设计模式中的装饰器模式，中间件本质是一个回调函数，参数包含请求对象request，响应对象response和执行下一个中间件的函数next。

在实现中间件时，单个中间件应该足够简单，职责单一。

```javascript
const Koa = require('koa');
const app = new Koa();

app.use(async (ctx, next) => {
  console.log(1)
  await next();
  console.log(2)
})

app.use((ctx, next) => {
  console.log(3)
  ctx.body = 'Hello, koa';
})

app.listen(3000)
// 打印 1 3 2
```

#### node中进程之间是如何通信的

node中创建一个进程，可以通过`child_process`模块的`fork()`方法，进程间通讯基于EventEmitter事件触发器，在子进程中使用`process.send()`发送消息，在父进程中调用`fork()`返回的子进程实例`on('message', callback)`方法监听消息。

```javascript
// index.js
const { fork } = require('node:child_process');

const si = fork('./subIndex.js');

si.on('message', (data) => {
  console.log(data); // 我是子进程
});

// subIndex.js
setTimeout(() => {
  process.send('我是子进程');
}, 1000);
```

#### process.nextTick(callback)、setImmediate(callback)和setTimeout(callback, 0)的区别？

✍️待补充

#### child_process模块中，spawn()、fork()、exec()的区别？

### ⭐️⭐️⭐️Hard

✍️待添加



<hr />

## 浏览器

### ⭐️Easy

#### 常见的浏览器内核有哪些?

#### DOMContentLoaded 与 load 的区别 ?

#### SPA单页应用的优缺点？

#### CSS加载会造成阻塞吗



### ⭐️⭐️Medium

#### 浏览器的主要组成部分是什么？

#### 为什么JS会阻塞页面加载

#### 说一说你对Cookie localStorage sessionStorage的理解

#### 讲讲浏览器缓存

#### 说一说从输入URL到页面呈现发生了什么？

#### 路由history和hash的区别？

#### 谈一谈你对重排和重绘理解

#### 谈一谈跨域，同源策略，以及跨域解决方案

#### 前端如何进行seo优化

#### requestAnimationFrame与requestIdleCallback区别





### ⭐️⭐️⭐️Hard

#### 浏览器的进程和线程

#### SSR的实现原理？




<hr />

## MVVM框架

### Vue

#### ⭐️Easy

##### 为什么 data 在组件内必须是函数，而 vue 的根实例则没有此限制？

##### vue 组件之间的通信

##### vue2和vue3的生命周期分别有哪些？

##### v-show与v-if区别



#### ⭐️⭐️Medium

##### 双向绑定的原理？

##### props 和 data 的优先级谁高？

##### 说下整个vue的渲染过程？

##### 说下nextTick原理？



#### ⭐️⭐️⭐️Hard

##### 你怎么理解 vue 中的 diff 算法？



### React

#### ⭐️Easy

✍️待添加

#### ⭐️⭐️Medium

✍️待添加

#### ⭐️⭐️⭐️Hard

✍️待添加



### 通用

#### ⭐️Easy

##### MVC和MVVM框架区别？

#### ⭐️⭐️Medium

✍️待添加

#### ⭐️⭐️⭐️Hard

✍️待添加



<hr />

## 前端工程化

### ⭐️Easy

✍️待添加



### ⭐️⭐️Medium

#### webpack 做过哪些优化，开发效率方面、打包策略方面等等

#### webpack中Loader和Plugins的区别

#### webpack plugins原理

#### webpack 热更新原理

#### webpack tree shaking原理

#### 动态导入原理

#### 谈谈你对source map的理解？

#### webpack中bundle、chunk、module的区别

#### webpack5新特性

#### npm管理痛点

#### 为什么 Vite 启动这么快？



### ⭐️⭐️⭐️Hard

✍️待添加



<hr />

## 前端优化

### ⭐️Easy

✍️待添加

### ⭐️⭐️Medium

#### 前端常见性能优化手段？

### ⭐️⭐️⭐️Hard

✍️待添加



<hr />

## 前端监控

### ⭐️Easy

✍️待添加

### ⭐️⭐️Medium

#### 前端如何做性能监控、异常监控？

### ⭐️⭐️⭐️Hard

✍️待添加



<hr />

## 前端安全

### ⭐️Easy

✍️待添加

### ⭐️⭐️Medium

#### 谈一谈你对XSS攻击理解

#### 谈一谈你对CSRF攻击理解

#### 谈谈你对sql注入的理解

### ⭐️⭐️⭐️Hard

✍️待添加

<hr />

## 跨端开发

### 微信小程序

#### ⭐️Easy

✍️待添加

#### ⭐️⭐️Medium

✍️待添加

#### ⭐️⭐️⭐️Hard

✍️待添加

### React Native

#### ⭐️Easy

✍️待添加

#### ⭐️⭐️Medium

✍️待添加

#### ⭐️⭐️⭐️Hard

✍️待添加

<hr />

## 计算机基础

### ⭐️Easy

#### 进程与线程的区别

### ⭐️⭐️Medium

#### 进程通信的几种方式

### ⭐️⭐️⭐️Hard

✍️待补充



<hr />

## 计算机网络

### ⭐️Easy

✍️待添加

### ⭐️⭐️Medium

#### TCP中三次握手和四次挥手的含义

#### Websocket与Ajax的区别？

### ⭐️⭐️⭐️Hard

✍️待添加

<hr />

## 数据结构和算法

### ⭐️Easy

#### 二叉树的遍历有几种方法？

### ⭐️⭐️Medium

#### 斐波那契数列实现

### ⭐️⭐️⭐️Hard

✍️待添加



<hr />

## 设计模式

### ⭐️Easy

✍️待添加

### ⭐️⭐️Medium

#### 谈谈常见的设计模式？

### ⭐️⭐️⭐️Hard

✍️待添加



<hr />

## 测试

### ⭐️Easy

✍️待添加

### ⭐️⭐️Medium

✍️待添加

### ⭐️⭐️⭐️Hard

✍️待添加



<hr />

## 手写函数

### ⭐️Easy

#### 防抖debounce

```javascript
const debounce = (fn, ms = 1000) => {
  let timer;
  return function (...args) {
    if (timer) {
      clearTimeout(timer);
    }
    timer = setTimeout(() => {
      fn.apply(this, args);
    }, ms);
  };
};
```

#### 节流throttle

```javascript
const throttle = (fn, ms = 1000) => {
  let flag = true;
  return function (...args) {
    if (!flag) return;
    flag = false;
    setTimeout(() => {
      fn.apply(this, args);
      flag = true;
    }, ms);
  };
};
```



#### New

```javascript
const New = (fn, ...args) => {
  const obj = {};
  if (fn.prototype) {
    Object.setPrototypeOf(obj, fn.prototype);
  }
  const res = fn.apply(obj, args);
  if (typeof res === 'function' || (typeof res === 'object' && res !== null)) {
    return res;
  }
  return obj;
};
```



#### 数组去重

```javascript
const uniqueArr = (arr) => {
  return [...new Set(arr)];
};
```



#### 实现正则切分千分位



### ⭐️⭐️Medium

#### bind

```javascript
Function.prototype.bind2 = function (context) {
  if (typeof this !== 'function') {
    throw new Error('not a function');
  }
  const fn = this;
  const args = Array.from(arguments).slice(1);
  const resFn = function () {
    // 如果是new调用，则绑定this为实例对象，也就是new创建的新对象，否则返回context
    return fn.apply(this instanceof resFn ? this : context, args.concat(...arguments));
  };

  // 返回的新函数的原型继承原函数的原型
  resFn.prototype = Object.create(fn.prototype);

  return resFn;
};
```

#### call

```javascript
Function.prototype.call2 = function (context = window) {
  // 创建唯一的key，在context对象上创建一个指向函数的变量
  const key = Symbol('key');
  context[key] = this;
  const args = [...arguments].slice(1);
  const res = context[key](...args);
  delete context[key];
  return res;
};
```

#### apply

```javascript
Function.prototype.apply2 = function (context = window) {
  const key = Symbol('key');
  context[key] = this;
  const res = arguments[1] ? context[key](...arguments[1]) : context[key]();
  delete context[key];
  return res;
};
```

#### 深拷贝

```javascript
const deepCopy = function (obj, cache = new WeakMap()) {
  if (!obj instanceof Object) return obj;

  // 返回循环引用
  if (cache.has(obj)) {
    console.log(cache.get(obj));
    return cache.get(obj);
  }

  // 支持函数
  if (obj instanceof Function) {
    return function () {
      return obj.apply(this, arguments);
    };
  }
  // 支持日期
  if (obj instanceof Date) return new Date(obj);
  // 支持正则
  if (obj instanceof RegExp) return new RegExp(obj.source, obj.flags);

  const res = Array.isArray(obj) ? [] : {};
  cache.set(obj, res);

  Object.keys(obj).forEach((key) => {
    if (obj[key] instanceof Object) {
      res[key] = deepCopy(obj[key], cache);
    } else {
      res[key] = obj[key];
    }
  });
  return res;
};
```

#### 柯里化

```javascript
const curry = function (fn) {
  return function curried(...args) {
    if (args.length >= fn.length) {
      return fn.apply(this, args);
    }
    return function (...args2) {
      // 将之前的参数和现在的参数拼接上
      return curried.apply(this, args.concat(args2));
    };
  };
};
```



#### 继承

es5继承

```javascript
function Person(name) {
  this.name = name;
}
Person.prototype.sayName = function () {
  console.log(this.name);
};
function Children(name, age) {
  Person.call(this, name);
  this.age = age;
}
Children.prototype.sayAge = function () {
  console.log(this.age);
};
Object.setPrototypeOf(Children.prototype, Person.prototype);
Children.prototype.constructor = Children;

const zs = new Children('张三', 20);
zs.sayName();
zs.sayAge();
```

es6继承

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }
  sayName() {
    console.log(this.name);
  }
  static callMe() {
    console.log('callMe');
  }
}
class Children extends Person {
  constructor(name, age) {
    super(name);
    this.age = age;
  }
  sayAge() {
    console.log(this.age);
  }
  static callMe() {
    console.log('callMe111');
  }
}

const zs = new Children('张三', 20);
zs.sayName();
zs.sayAge();
Children.callMe();
```



#### instanceof

```javascript
const _instanceOf = (left, right) => {
  let proto = left.__proto__;
  const prototype = right.prototype;
  while (true) {
    if (proto === null) return false;
    if (proto === prototype) return true;
    proto = proto.__proto__;
  }
};
```



#### 数组扁平化

```javascript
function flatter(arr) {
  if (!arr.length) return;
  return arr.reduce((pre, cur) => (Array.isArray(cur) ? [...pre, ...flatter(cur)] : [...pre, cur]), []);
}
```



#### 对象扁平化

```javascript
const flatter = (obj) => {
  const res = {};
  const process = (key, value) => {
    if (typeof value !== 'object') {
      res[key] = value;
    } else if (Object.prototype.toString.call(value) === '[object Object]') {
      const keyArr = Object.keys(value);
      keyArr.forEach((item) => {
        process(key ? `${key}.${item}` : `${item}`, value[item]);
      });
    } else if (Object.prototype.toString.call(value) === '[object Array]') {
      value.forEach((item, index) => {
        process(`${key}[${index}]`, item);
      });
    }
  };
  process('', obj);
  return res;
};
```



#### JSON.parse

```javascript
const parse = (target) => {
  return eval(`(${target})`);
};
```



#### JSON.stringify

```javascript
function getType(o) {
  return typeof o === 'symbol' ? 'Symbol_basic' : Object.prototype.toString.call(o).slice(8, -1);
}
function isObject(o) {
  return o !== null && (typeof o === 'object' || typeof o === 'function');
}
function processOtherTypes(target, type) {
  switch (type) {
    case 'String':
      return `"${target.valueOf()}"`;
    case 'Number':
    case 'Boolean':
      return target.valueOf().toString();
    case 'Symbol':
    case 'Error':
    case 'RegExp':
      return '{}';
    case 'Date':
      return `"${target.toJSON()}"`;
    case 'Function':
      return undefined;
    default:
      return null;
  }
}
function checkCircular(obj, currentParent) {
  let type = getType(obj);
  if (type == 'Object' || type == 'Array') {
    if (currentParent.includes(obj)) {
      throw new TypeError('Converting circular structure to JSON');
    }
    currentParent.push(obj);
  }
}
function jsonStringify(target, initParent = [target]) {
  let type = getType(target);
  let iterableList = ['Object', 'Array', 'Arguments', 'Set', 'Map'];
  let specialList = ['Undefined', 'Symbol_basic', 'Function'];
  if (!isObject(target)) {
    // symbol和undefined返回undefined
    if (type === 'Symbol_basic' || type === 'Undefined') {
      return undefined;
    }
    // NaN、Infinity和-Infinity返回"null"
    else if (Number.isNaN(target) || target === Infinity || target === -Infinity) {
      return 'null';
    }
    // string返回"string"
    else if (type === 'String') {
      return `"${target}"`;
    }
    return String(target);
  } else {
    let res;
    if (!iterableList.includes(type)) {
      // 其他对象类型
      res = processOtherTypes(target, type);
    } else {
      // 数组
      if (type === 'Array') {
        res = target.map((item) => {
          if (specialList.includes(getType(item))) {
            return 'null';
          } else {
            let currentParent = [...initParent];
            checkCircular(item, currentParent);
            return jsonStringify(item, currentParent);
          }
        });
        res = `[${res}]`.replace(/'/g, '"');
      } else {
        // Object
        res = [];
        Object.keys(target).forEach((key) => {
          if (getType(key) !== 'Symbol_basic') {
            let type = getType(target[key]);
            if (!specialList.includes(type)) {
              let currentParent = [...initParent];
              checkCircular(target[key], currentParent);
              res.push(`"${key}":${jsonStringify(target[key], currentParent)}`);
            }
          }
        });
        res = `{${res}}`.replace(/'/g, '"');
      }
    }
    return res;
  }
}
```



#### 事件触发器

```javascript
class EventEmitter {
  cache: Record<string, Function[]> = {};
  on(name: string, fn: Function) {
    const tasks = this.cache[name];
    if (!tasks) {
      this.cache[name] = [fn];
    } else {
      this.cache[name].push(fn);
    }
  }
  emit(name: string, once = false) {
    const tasks = this.cache[name].slice();
    if (tasks) {
      tasks.forEach((fn) => {
        fn();
      });
      if (once) {
        delete this.cache[name];
      }
    }
  }
  off(name: string, fn: Function) {
    const tasks = this.cache[name];
    if (tasks) {
      const index = tasks.findIndex((f) => f === fn);
      if (index !== -1) {
        tasks.splice(index, 1);
      }
    }
  }
}
```



#### 简单实现async/await中的async函数

```javascript
const async = (genertor) => {
  const iterator = genertor();

  function handle(iteratorResult) {
    if (iteratorResult.done) return;
    const itertorValue = iteratorResult.value;
    if (itertorValue instanceof Promise) {
      itertorValue.then((res) => handle(iterator.next(res))).catch((err) => iterator.throw(err));
    }
  }

  try {
    handle(iterator.next());
  } catch (error) {
    iterator.throw(error);
  }
};
```



#### 实现正则获取url params

✍️待补充

#### 实现jsonp

✍️待补充



### ⭐️⭐️⭐️Hard

#### Promise

```javascript
const PENDING = 'pending';
const FULFILLED = 'fulfilled';
const REJECTED = 'rejected';

const resolvePromise = (promise2, x, resolve, reject) => {
  if (promise2 === x) {
    return reject('111111');
  }
  if (x instanceof promise2) {
    x.then(resolve, reject);
  } else {
    resolve(x);
  }
};

class MyPromise {
  constructor(fn) {
    try {
      fn(this.resolve, this.reject);
    } catch (err) {
      this.reject(err);
    }
  }

  status = PENDING;
  value = null;
  reason = null;
  fulfilledList = [];
  rejectedList = [];

  resolve = (val) => {
    if (this.status === PENDING) {
      this.status = FULFILLED;
      this.value = val;
      while (this.fulfilledList.length) {
        this.fulfilledList.shift()(this.val);
      }
    }
  };

  reject = (reason) => {
    if (this.status === PENDING) {
      this.status = REJECTED;
      this.reason = reason;
      while (this.rejectedList.length) {
        this.rejectedList.shift()(this.reason);
      }
    }
  };

  then(fulfilledCallback, rejectedCallback) {
    const realFulfilledCallback = typeof fulfilledCallback === 'function' ? fulfilledCallback : (val) => val;
    const realRejectedCallback =
          typeof rejectedCallback === 'function'
    ? rejectedCallback
    : (reason) => {
      throw reason;
    };

    const promise2 = new MyPromise((resolve, reject) => {
      const microResolve = () => {
        queueMicrotask(() => {
          try {
            const x = realFulfilledCallback(this.value);
            resolvePromise(promise2, x, resolve, reject);
          } catch (err) {
            reject(err);
          }
        });
      };
      const microReject = () => {
        queueMicrotask(() => {
          try {
            const x = realRejectedCallback(this.reason);
            resolvePromise(promise2, x, resolve, reject);
          } catch (err) {
            reject(err);
          }
        });
      };

      if (this.status === FULFILLED) {
        microResolve();
      } else if (this.status === REJECTED) {
        microReject();
      } else {
        this.fulfilledList.push(microResolve);
        this.rejectedList.push(microReject);
      }
    });
    return promise2;
  }

  catch = (rejectedCallback) => {
    this.then(null, rejectedCallback);
  };

  static resolve(val) {
    return new MyPromise((resolve) => {
      resolve(val);
    });
  }

  static reject(reason) {
    return new MyPromise((resolve, reject) => {
      reject(reason);
    });
  }

  static all(list) {
    let resList = [];
    let count = 0;
    return new MyPromise((resolve, reject) => {
      for (let i = 0; i < list.length; i++) {
        list[i]
          .then((val) => {
          resList[i] = val;
          count++;
          if (count === list.length) {
            resolve(resList);
          }
        })
          .catch((err) => {
          reject(err);
        });
      }
    });
  }

  static rare(list) {
    return new MyPromise((resolve, reject) => {
      for (let i = 0; i < list.length; i++) {
        list[i]
          .then((val) => {
          resolve(val);
        })
          .catch((err) => {
          reject(err);
        });
      }
    });
  }
}
```

