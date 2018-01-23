# JavaScript 编程规范

### 1 代码注释规范

代码注释在编程中非常重要

#### 1.1 文件注释

文件注释位于文件的最前面，应包括文件的以下信息：
1.概要说明及版本（必须）项目地址（开源组件必须）版权声明（必须）开源协议（开源组件必须）版本号（必须）修改时间（必须），以ISO格式表示（可使用Sublime Text的InsertDate插件插入）文件注释必须全部以英文字符表示，并存在于文件的开发版本与生产版本中

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

如果文件内包含了一些开源组件，则必须在文件注释中进行说明

``` javascript
// Include JQuery (http://xxx.com/)
```

#### 1.2 文件注释

普通注释是为了帮助开发者和阅读者更好地理解程序，不会出现在API文档中。其中，单行注释以`//`开头；多行注释以`/*`开头，以`*/`结束。普通注释的使用需遵循以下规定

a) 单行注释后留一个空格

```javascript
// this is a comment
```

b) 多行注释星号对齐

```javascript
/* 
this is a comment
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