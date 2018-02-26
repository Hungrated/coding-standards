# JavaScript 编程规范

### 1 代码注释

代码注释在编程中非常重要

#### 1.1 文件注释

文件注释位于文件的最前面，应包括文件的以下信息：  

1. 概要说明及版本（必须）项目地址（开源组件必须）版权声明（必须）开源协议（开源组件必须）版本号（必须）修改时间（必须），以ISO格式表示（可使用Sublime Text的InsertDate插件插入）文件注释必须全部以英文字符表示，并存在于文件的开发版本与生产版本中

``` javascript
/*!
 *
 * Some Javascript Library
 *
 * hungrat-plus - v1.0.0 (2018-01-22T14:55:51+0800)
 *
 * http://xxx.cn/ | Released under MIT license
 */
```

2. 如果文件内包含了一些开源组件，则必须在文件注释中进行说明

``` javascript
// Include JQuery (http://xxx.com/)
```

#### 1.2 普通注释

普通注释是为了帮助开发者和阅读者更好地理解程序，不会出现在API文档中。其中，单行注释以`//`开头；多行注释以`/*`开头，以`*/`结束。普通注释的使用需遵循以下规定

a) 单行注释后留一个空格

```javascript
// this is a comment
```

b) 多行注释星号对齐

```javascript
/* 
 * this is a comment
 */
```

c) 不要把注释写在多行注释的开始符、结束符所在行

```javascript
/*
 * start
 *   this is a correct comment                          
 * end
 */
```

d) 不要编写无意义的注释

> 如果某段代码有功能未实现，或者有待完善，必须添加“TODO”标记，“TODO”前后应留一个空格

```javascript
// TODO 未处理IE6-8的兼容性
function setOpacity(node, val) {
    node.style.opacity = val;
}
```

#### 1.3 文档注释

文档注释将会以预定格式出现在API文档中。它以`/**`开头，以`*/`结束，其间的每一行均以`*`开头（均与开始符的第一个`*`对齐），且注释内容与`*`间留一个空格

```javascript
/**
 *
 * comment
 */
```

文档注释必须包含一个或多个注释标签

a) @module 声明模块

```javascript
/**
 *
 * 模块说明
 *
 * @module 模块名
 */
```

b) @class 声明类

```javascript
/**
 *
 * 类说明
 *
 * @class 类名
 *
 * @constructor
 */
```

> @class必须搭配@constructor或@static使用，分别标记非静态类与静态类

c) @method 声明函数或类方法

```javascript
/**
 *
 * 方法说明
 *
 * @method 方法名
 *
 * @for 所属类名
 *
 * @param {参数类型} 参数名 参数说明
 *
 * @return {返回值类型} 返回值说明
 */
```

> 没有指定@for时，表示此函数为全局或模块顶层函数。当函数为静态函数时，必须添加@static；当函数有参数时，必须使用@param；当函数有返回值时，必须使用@return

d) @param 声明函数参数（必须与@method搭配使用）

当参数出现以下情况时，使用对应的格式:  
  `[参数名]` 无默认值时  
  `[参数名 = 默认值]` 有默认值时

e) @property 声明模块

```javascript
/**
 *
 * 属性说明
 *
 * @property {属性类型} 属性名
 */
```

f) @api 声明接口

例子如下

```javascript
/**
 *
 * 接口说明
 *
 * @api {get} /user/import
 * @apiName userImport
 * @apiGroup Netease
 * 
 * @apiParam {String} username Name of a user.
 * @apiParam {String} password Password of a user.
 * 
 * @apiSuccess {JSONP} data Response data.
 * 
 */
```

> 更多类型，参考链接：http://apidocjs.com/#param-api


### 2 常用内置对象

#### 2.1 `Array` 数组对象

数组是类似于列表的高阶对象。  

##### 2.1.1 `Array.of()` | 创建新实例 | `不改变原数组`
 
* `Array.of()` 方法创建一个具有可变数量参数的新数组实例，而不考虑参数的数量或类型。

* `Array.of()` 和 `Array` 构造函数之间的区别在于处理整数参数：`Array.of(7)` 创建一个具有单个元素 7 的数组，
而 `Array(7)` 创建一个包含 7 个 undefined 元素的数组。

##### 2.1.2 `Array.prototype.concat(value1[, value2[, ...[, valueN]]])` | 合并数组 | `不改变原数组`

* `concat()` 方法用于合并两个或多个数组。此方法不会更改现有数组，而是返回一个新数组。

* **注意**：数组/值在连接时保持不变。此外，对于新数组的任何操作（仅当元素不是对象引用时）都不会对原始数组产生影响，反之亦然。

##### 2.1.3 `Array.prototype.copyWithin(target[, start[, end]])` | 浅复制部分内容到同数组另一位置 | `ES6` `改变原数组`

* `copyWithin()` 方法浅复制数组的一部分到同一数组中的另一个位置，并返回它，而不修改其大小。

##### 2.1.4 `Array.prototype.fill(value[, start[, end]])` | 填充数组 | `ES6`

* `fill()` 方法用一个固定值填充一个数组中从起始索引到终止索引内的全部元素。

##### 2.1.5 `Array.prototype.filter(callback[, thisArg])` | 过滤数组 | `不改变原数组`

* `filter()` 方法创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。参考：2.1.5

##### 2.1.6 `Array.prototype.find(callback[, thisArg])` | 寻找指定值 | `ES6` `不改变原数组`

* `find()` 方法返回数组中满足提供的测试函数的第一个元素的**值**。否则返回 `undefined`。

##### 2.1.7 `Array.prototype.findIndex(callback[, thisArg])` | 寻找指定索引 | `ES6` `不改变原数组`

* `findIndex()` 方法返回数组中满足提供的测试函数的第一个元素的**索引**。否则返回-1。

##### 2.1.8 `Array.prototype.forEach(callback(currentValue, index, array){}, this)` | 遍历执行 | `ES5`

* `forEach()` 方法对数组的每个元素执行一次提供的函数。

##### 2.1.9 `Array.prototype.includes(searchElement[, fromIndex])` | 判断包含 | `ES7`

* `includes()` 方法用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 true ，否则返回 false 。

##### 2.1.10 `Array.prototype.indexOf()` | 寻找元素索引 | `ES5`

* `indexOf()` 方法返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1。

##### 2.1.11 `Array.prototype.join([separator = ','])` | 连接元素 | `不改变原数组`

* `join()` 方法将一个数组（或一个类数组对象）的所有元素连接成一个字符串并返回这个字符串。

##### 2.1.12`Array.prototype.keys()` | 数组迭代器 | `ES6` `不改变原数组`

##### 2.1.13 `Array.prototype.lastIndexOf(searchElement[, fromIndex = arr.length - 1])` | 最后索引 | `ES5`

* `lastIndexOf()` 方法返回指定元素（也即有效的 JavaScript 值或变量）在数组中的最后一个的索引，
如果不存在则返回 -1。从数组的后面向前查找，从 `fromIndex` 处开始。

##### 2.1.14 `Array.prototype.map(function callback(currentValue, index, array) {}[, thisArg])` | 数组映射 | `不改变原数组`

* `map()` 方法创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。

##### 2.1.15 `Array.prototype.pop()` | 数组末尾删除单元素 | `改变原数组`

* `pop()` 方法从数组中删除最后一个元素，并返回该元素的值。此方法更改数组的长度。

##### 2.1.16 `Array.prototype.push(element1[, element2[, ...[, elementN]]])` | 数组末尾增加元素 | `改变原数组`

* `push()` 方法将一个或多个元素添加到数组的末尾，并返回新数组的长度。

* 当调用该方法时，新的 `length` 属性值将被返回。

##### 2.1.17 `Array.prototype.reduce(callback[, initialValue])` | 减少为单个值 | `ES5`

* `reduce()` 方法对累加器和数组中的每个元素（从左到右）应用一个函数，将其减少为单个值。

##### 2.1.18 `Array.prototype.reduceRight(callback[, initialValue])` | 从右开始减少为单个值 | `ES5`

reduceRight() 方法接受一个函数作为累加器（accumulator）和数组的每个值
（从右到左）将其减少为单个值（与 `Array.prototype.reduce()` 的执行方向相反）。

##### 2.1.19 `Array.prototype.reverse()` | 颠倒数组 | `改变原数组`

* `reverse()` 方法将数组中元素的位置颠倒。第一个数组元素成为最后一个数组元素，最后一个数组元素成为第一个。

##### 2.1.20 `Array.prototype.shift()` | 删除并返回数组首元素 | `改变原数组`

* `shift()` 方法从数组中删除第一个元素，并返回该元素的值。此方法更改数组的长度。

##### 2.1.21 `Array.prototype.unshift(element1[, element2[, ...[, elementN]]])` | 添加首元素 | `改变原数组`

* `unshift()` 方法将一个或多个元素添加到数组的开头，并返回新数组的长度。

* 当调用该方法时，新的 `length` 属性值将被返回。

##### 2.1.22 `Array.prototype.slice([start[, end]])` | 截取数组 | `不改变原数组`

* `slice()` 方法返回一个从开始到结束（不包括结束）选择的数组的一部分浅拷贝到一个新数组对象。原始数组不会被修改。

##### 2.1.23`Array.prototype.some(callback[, thisArg])` | 测试数组 | `ES5`

* `some()` 方法测试数组中的某些元素是否通过由提供的函数实现的测试（是否**存在**元素符合条件）。

##### 2.1.24 `Array.prototype.every(callback[, thisArg])` | 测试数组 | `ES5`

* `every()` 方法测试数组的所有元素是否都通过了指定函数的测试（是否**任意**元素符合条件）。

##### 2.1.25 `Array.prototype.sort([compareFunction])` | 数组排序 | `改变原数组`

* `sort()` 方法用就地（ in-place ）的算法对数组的元素进行排序，并返回数组。
sort 排序不一定是稳定的。默认排序顺序是根据字符串Unicode码点。

##### 2.1.26 `Array.prototype.splice(start[, deleteCount[, item1[, item2[, ...[, itemN]]]]])` | 更改数组 | `改变原数组`

* `splice()` 方法通过删除现有元素和/或添加新元素来更改一个数组的内容。

##### 2.1.27 `Array.prototype.toLocaleString([locales[,options]])` | 转换为字符串 | `不改变原数组`

* `toLocaleString()` 返回一个字符串表示数组中的元素。数组中的元素将使用各自的 toLocaleString 方法转成字符串，
这些字符串将使用一个特定语言环境的字符串（例如一个逗号 ","）隔开。

##### 2.1.28 `Array.prototype.concat()` | 转换为字符串 | `不改变原数组`

* `toString()` 返回一个字符串，表示指定的数组及其元素（元素用逗号连接）。

* 从 JavaScript 1.8.5 (Firefox 4) 开始，和 ECMAScript 第5版语义（semantics）一致，toString() 方法是通用的，
可被用于任何对象。如果对象有一个 join() 方法，将会被调用，其返回值将被返回。没有则调用 Object.prototype.toString() 方法。

##### 2.1.29`Array.prototype.entries()` | 迭代器入口 | `ES6`

* `entries()` 方法返回一个新的Array Iterator对象，
该对象包含数组中每个索引的**键/值对**（`console.log(iterator.next().value);`）。

##### 2.1.30 `Array.prototype.values()` | 迭代器入口 | `ES6`

* `values()` 方法返回一个新的Array Iterator对象，该对象包含数组中每个索引的**值**（`console.log(iterator.next().value);`）。

* Chrome 未实现，Firefox未实现，Edge已实现。

##### 2.1.31 `Array.prototype.@@iterator()` | 迭代器 | `ES6`

* `@@iterator` 属性和 `values()` 属性的初始值均为同一个函数对象（`arr[Symbol.iterator]()`）。

