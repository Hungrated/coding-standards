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

#### 2.2 `String` 字符串对象

String 全局对象是一个用于字符串或一个字符序列的构造函数。

##### 2.2.1 `String.prototype.charAt(index)` | 返回指定字符 | `不改变原字符串`

##### 2.2.2 `String.prototype.concat(string2[, string3[, ..., stringN]])` | 连接字符串 | `不改变原字符串`

* `concat()` 方法将一个或多个字符串与原字符串连接合并，形成一个新的字符串并返回。

##### 2.2.3 `String.prototype.includes(searchString[, position])` | 判断包含 | `ES6`

* `includes()` 方法用于判断一个字符串是否包含在另一个字符串中，根据情况返回 `true` 或 `false` 。

##### 2.2.4 `String.prototype.indexOf(searchValue[, fromIndex])` | 返回指定索引 | `不改变原字符串`

* `indexOf()` 方法返回调用 `String` 对象中第一次出现的指定值的索引，开始在 fromIndex进行搜索。如果未找到该值，则返回-1。

##### 2.2.5 `String.prototype.lastIndexOf(searchValue[, fromIndex])` | 返回指定索引 | `不改变原字符串`

* `lastIndexOf()` 方法返回指定值在调用该方法的字符串中最后出现的位置，如果没找到则返回 -1。
从该字符串的后面向前查找，从 fromIndex 处开始。

##### 2.2.6 `String.prototype.localeCompare(compareString[, locales[, options]])` | 比较字符串 | `ES6`

* `localeCompare()` 方法返回一个数字来指示一个参考字符串是否在排序顺序前面或之后或与给定字符串相同。
新的 `locales` 、 `options` 参数能让应用程序定制函数的行为即指定用来排序的语言。
`locales` 和 `options` 参数是依赖于具体实现的，在旧的实现中这两个参数是完全被忽略的。

##### 2.2.7 `String.prototype.match(regexp)` | 返回匹配字符 | `不改变原字符串`

* 当一个字符串与一个正则表达式匹配时， `match()` 方法检索匹配项。

* 如果正则表达式不包含 `g` 标志，则 `str.match()` 会返回和 `RegExp.exec()` 相同的结果。
而且返回的 `Array` 拥有一个额外的 `input` 属性，该属性包含被解析的原始字符串。
另外，还拥有一个 `index` 属性，该属性表示匹配结果在原字符串中的索引（以0开始）。
  
* 如果正则表达式包含 `g` 标志，则该方法返回一个 `Array` ，它包含所有匹配的子字符串而不是匹配对象。
捕获组不会被返回(即不返回index属性和input属性)。如果没有匹配到，则返回 `null` 。

##### 2.2.8 `String.prototype.normalize([form = 'NFC'])` | 正规化字符串 | `ES6`

* `normalize()` 方法会按照指定的一种 Unicode 正规形式将当前字符串正规化。

##### 2.2.9 `String.prototype.padStart(targetLength [, padString])` | 首部填充字符 | `ES8` `改变原字符串`

* `padStart()` 方法用另一个字符串填充当前字符串(重复，如果需要的话)，以便产生的字符串达到给定的长度。
填充从当前字符串的开始(左侧)应用的。

##### 2.2.10 `String.prototype.padEnd(targetLength [, padString])` | 尾部填充字符 | `ES8` `改变原字符串`

* `padEnd()` 方法会用一个字符串填充当前字符串（如果需要的话则重复填充），返回填充后达到指定长度的字符串。
从当前字符串的末尾（右侧）开始填充。

##### 2.2.11 `String.prototype.repeat(count)` | 复制字符串 | `ES6` `不改变原字符串`

* `repeat()` 构造并返回一个新字符串，该字符串包含被连接在一起的指定数量的字符串的副本。

##### 2.2.12 `String.prototype.replace(regexp|substr, newSubStr|function)` | 匹配并替换字符串 | `不改变原字符串`

* `replace()` 方法返回一个由替换值替换一些或所有匹配的模式后的新字符串。
模式可以是一个字符串或者一个正则表达式, 替换值可以是一个字符串或者一个每次匹配都要调用的函数。

* 注意：原字符串不会改变。

##### 2.2.13 `String.prototype.search(regexp)` | 搜索正则匹配 | `不改变原字符串`

* `search()` 方法执行正则表达式和 `String` 对象之间的一个搜索匹配。

##### 2.2.14 `String.prototype.slice(beginSlice[, endSlice])` | 截取字符串 | `不改变原字符串`

* `slice()` 方法提取一个字符串的一部分，并返回一新的字符串。

##### 2.2.15 `String.prototype.split([separator[, limit]])` | 分割为字符串数组 | `不改变原字符串`

* `split()` 方法使用指定的分隔符字符串将一个 `String` 对象分割成字符串数组，以将字符串分隔为子字符串，以确定每个拆分的位置。

* 如果空字符串("")被用作分隔符，则字符串会在每个字符之间分割。

* 当字符串为空时，`split()` 返回一个包含一个空字符串的数组，而不是一个空数组，如果字符串和分隔符都是空字符串，则返回一个空数组。

##### 2.2.16 `String.prototype.startsWith(searchString [, position])` | 判断以指定字符串为首 | `ES6`

* `startsWith()` 方法用来判断当前字符串是否是以另外一个给定的子字符串“开头”的，根据判断结果返回 `true` 或 `false`。

##### 2.2.17 `String.prototype.endsWith(searchString [, position])` | 判断以指定字符串为尾 | `ES6`

* `endsWith()` 方法用来判断当前字符串是否是以另外一个给定的子字符串“结尾”的，根据判断结果返回 `true` 或 `false`。

##### 2.2.18 `String.prototype.substr(start[, length])` | 返回指定字符 | `不改变原字符串`

* `substr()` 方法返回一个字符串中从指定位置开始到指定字符数的字符。

##### 2.2.19 `String.prototype.substring(indexStart[, indexEnd])` | 返回指定字符 | `不改变原字符串`

* `substring()` 方法返回一个字符串在开始索引到结束索引之间的一个子集, 或从开始索引直到字符串的末尾的一个子集。

##### 2.2.20 `String.prototype.toLowerCase()` | 改为全小写 | `不改变原字符串`

* `toLowerCase()` 会将调用该方法的字符串值转为小写形式，并返回。

##### 2.2.21 `String.prototype.toLowerCase()` | 改为全大写 | `不改变原字符串`

* `toUpperCase()` 会将调用该方法的字符串值转为大写形式，并返回。

##### 2.2.22 `String.prototype.toString()` | 返回指定对象字符串形式 | `不改变原字符串`

##### 2.2.23 `String.prototype.trim()` | 删除两端空白字符 | `ES5` `改变原字符串`

* `trim()` 方法会从一个字符串的两端删除空白字符。在这个上下文中的空白字符是所有的空白字符
 (space, tab, no-break space 等) 以及所有行终止符字符（如 LF，CR）。

##### 2.2.24 `String.prototype[@@iterator]()` | 迭代器 | `ES6`

* `[@@iterator]()` 方法返回一个新的Iterator对象，它遍历字符串的代码点，返回每一个代码点的字符串值。

##### 2.2.25 ``String.raw `templateString` `` | 返回字符串原始字面量 | `ES6`

* `String.raw()` 是一个模板字符串的标签函数，它的作用类似于 Python 中的
字符串前缀 r 和 C# 中的字符串前缀 @，是用来获取一个模板字符串的原始字面量值的。

#### 2.3 `Number` 数字对象

##### 2.3.1 `Number.isFinite(value)` | 是否有穷数

* `value` 只有数值类型的值，且是有穷的（finite），才返回 true。

##### 2.3.2 `Number.isInteger(value)` | 是否整数

* 注意 `NaN` 和正负 `Infinity` 不是整数。

##### 2.3.3 `Number.isNaN(value)` | 是否非数字

* 在 JavaScript 中，`NaN` 最特殊的地方就是，我们不能使用相等运算符（ `==` 和 `===` ）来判断一个值是否是  `NaN`，因为 `NaN == NaN` 和 `NaN === NaN` 都会返回 `false`。因此，必须要有一个判断值是否是 `NaN` 的方法。
  
* 和全局函数 `isNaN()` 相比，该方法不会强制将参数转换成数字，只有在参数是真正的数字类型，且值为 `NaN` 的时候才会返回 `true`。

##### 2.3.4 `Number.parseFloat(string)` | 转换为浮点数 | `ES6`

* `Number.parseFloat()` 方法可以把一个字符串解析成浮点数。该方法与全局的 `parseFloat()` 函数相同，并且处于 ECMAScript 6 规范中（用于全局变量的模块化）。

##### 2.3.5 `Number.parseInt(string[, radix])` | 转换为整数 | `ES6`

* `Number.parseInt()` 方法可以根据给定的进制数把一个字符串解析成整数。可选择进制。

##### 2.3.6 `Number.prototype.toExponential(fractionDigits)` | 指数表示法

* `toExponential(` 方法以指数表示法返回该数值字符串表示形式。

##### 2.3.7 `Number.prototype.toFixed(digits)` | 定点表示法

* `toFixed()` 方法使用定点表示法来格式化一个数。

##### 2.3.8 `Number.prototype.toPrecision(precision)` | 有效数字表示

* `toPrecision()` 方法以指定的精度返回该数值对象的字符串表示。

##### 2.3.9 `Number.prototype.toString([radix])` | 转换成字符串

#### 2.4 `Date` 日期对象

参考：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date

#### 2.5 `Math` 数学对象

参考：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math

### 3 Google最新JavaScript标准

* 使用空格代替tab

> 除了每一行的终止符序列，ASCII水平空格符（0x20）是唯一一个可以出现在源文件中任意位置的空格字符。这也意味着，tab字符不应该被使用，以及被用来控制缩进。

规范随后指出应该使用2个，而不是4个空格带实现缩进。

* 不能省略分号

> 每个语句必须以分号结尾。不允许依赖于JS自动添加分号的功能。

尽管我不明白为什么会有人反对这个规则，但目前分号的使用问题显然已经像“空格 vs tab”这个问题一样产生了巨大的争议。而Google对此表示分号是必须的，是不可省略的。

* 不推荐代码水平对齐

> Google的代码规范允许但不推荐对代码进行水平对齐。即使之前的代码中做了水平对齐的处理，以后也应该避免这种行为。

对代码进行水平对齐会在代码中添加若干多余的空格，这让相邻两行的字符看上去处于一条垂直线上。

* 杜绝var

> 使用const或let来声明所有局部变量。如果变量不需要被重新赋值，默认应该使用const。应该拒绝使用关键字var。

我不知道是因为没有人能说服他们，还是说因为旧习难改。目前我仍能看到许多人在StackOverFlow或其他地方使用var声明变量。

* 优先使用箭头函数

> 箭头函数提供了一种简洁的语法，并且避免了一些关于this指向的问题。相比较与function关键字，开发者应该优先使用箭头函数来声明函数，尤其是声明嵌套函数。

坦白说，我曾以为箭头函数的作用只在于简洁美观。但现在我发现原来它们还有更重要的作用。

* 使用模板字符串取代连接字符串

> 在处理多行字符串时，模板字符串比复杂的拼接字符串要表现得更出色。

* 不要使用续行符分割长字符串

> 在JS中，\也代表着续行符。Google的代码规范不允许在不管是模板字符串还是普通字符串中使用续行符。尽管ES5中允许这么做，但如果在\后跟着某些结束空白符，这种行为会导致一些错误，而这些错误在审阅代码时很难注意到。

* 优先使用`for...of`

> 在ES6中，有3种不同的for循环。尽管每一种有它的应用场景，但Google仍推荐使用`for...of`。

真有趣，Google居然会特别指定一种for循环。虽然这很奇怪，但不影响我接受这一观点。

以前我认为for...in适合遍历Object，而for...of适合遍历数组。因为我喜欢这种各司其职的使用方式。

尽管Google的规范与这种使用方式相冲突，但Google对for...of的偏爱依然让我觉得十分有趣。

* 不要使用eval语句

> 除非是在code loader中，否则不用使用eval或是Function(...string)结构。这个功能具有潜在的危险性，并且在CSP环境中无法起作用。

MDN中有一节专门提到不要使用eval语句。

* 常量的命名规范

> 常量命名应该使用全大写格式，并用下划线分割

如果你确定一定以及肯定一个变量值以后不会被修改，你可以将它的名称使用全大写模式改写，暗示这是一个常量，请不要修改它的值。

遵守这条规则时需要注意的一点是，如果这个常量是一个函数，那么应该使用驼峰式命名法。

* 每次只声明一个变量

> 每一个变量声明都应该只对应着一个变量。不应该出现像`let a = 1,b = 2;`这样的语句。

* 使用单引号

> 只允许使用单引号包裹普通字符串，禁止使用双引号。如果字符串中包含单引号字符，应该使用模板字符串。

**参考资料**：http://mp.weixin.qq.com/s/itTcxdyEYi0anUPBIRhYsw
