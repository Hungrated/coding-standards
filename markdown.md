# Markdown 语法规范

### 1 标题

Markdown 标题支持两种形式：

a) 用 `#` 标记

在 标题开头 加上1~6个 `#` ，依次代表一级标题、二级标题……六级标题

```markdown
# 一级标题
## 二级标题
### 三级标题
##### 四级标题
###### 五级标题
###### 六级标题

# 一级标题 #
## 二级标题 ##
### 三级标题 ###
#### 四级标题 ####

```

b) 用 `=` 和 `-` 标记

在 标题底下 加上任意个 `=` 代表一级标题， `-` 代表二级标题

```markdown
一级标题
======

二级标题
----------
```

### 2 列表

Markdown 支持有序列表和无序列表。

无序列表使用 `-` 、 `+` 和 `*` 作为列表标记

```markdown
- Red
- Green
- Blue

* Red
* Green
* Blue

+ Red
+ Green
+ Blue
```

有序列表则使用数字加英文句点 `.` 来表示

```markdown
1. Red
2. Green
3. Blue
```

### 3 引用

引用以 `>` 来表示，引用中支持多级引用、标题、列表、代码块、分割线等常规语法

```
> 这是一段引用    //在`>`后面有 1 个空格
> 
>     这是引用的代码块形式    //在`>`后面有 5 个空格
>     
> 代码例子：
>   
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

> 一级引用
> > 二级引用
> > > 三级引用

> #### 这是一个四级标题
> 
> 1. 这是第一行列表项
> 2. 这是第二行列表项

```

效果如下

> 这是一段引用    //在`>`后面有 1 个空格
> 
>     这是引用的代码块形式    //在`>`后面有 5 个空格
>     
> 代码例子：
>   
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

> 一级引用
> > 二级引用
> > > 三级引用

> #### 这是一个四级标题
> 
> 1. 这是第一行列表项
> 2. 这是第二行列表项


### 4 强调

两个 `*` 或-代表加粗，一个 `*` 或 `-` 代表斜体， `~~` 代表删除

```markdown
**加粗文本** 或者 __加粗文本__

*斜体文本*  或者_斜体文本_

~~删除文本~~
```

效果如下

**加粗文本** 或者 __加粗文本__

*斜体文本*  或者_斜体文本_

~~删除文本~~


### 5 图片与链接

图片与链接的语法很像，区别在一个 ! 号。二者格式

```markdown
图片：![]()    ![图片文本(可忽略)](图片地址)

链接：[]()     [链接文本](链接地址)
```

链接又分为`行内式`、`参考式`和`自动链接`

```markdown
这是行内式链接：[Hungrated](https://github.com/Hungrated)。

这是参考式链接：[Hungrated][url]，其中url为链接标记，可置于文中任意位置。

[url]: https://github.com/Hungrated "Hungrated"

链接标记格式为：[链接标记文本]:  链接地址  链接title(可忽略)

这是自动链接：直接使用`<>`括起来<https://github.com/Hungrated>

这是图片：![][avatar]

[avatar]: https://avatars2.githubusercontent.com/u/25450771?s=400&u=e26233c729fc9354c09911ad8d85757a9a279171&v=4
```

效果如下

这是行内式链接：[Hungrated](https://github.com/Hungrated)。

这是参考式链接：[Hungrated][url]，其中url为链接标记，可置于文中任意位置。

[url]: https://github.com/Hungrated "Hungrated"

链接标记格式为：[链接标记文本]:  链接地址  链接title(可忽略)

这是自动链接：直接使用`<>`括起来<https://github.com/Hungrated>

这是图片：![][avatar]

[avatar]: https://avatars2.githubusercontent.com/u/25450771?s=400&u=e26233c729fc9354c09911ad8d85757a9a279171&v=4

### 6 代码

代码分为`行内代码`和`代码块`

行内代码使用 `代码` 标识，可嵌入文字中

代码块使用4个空格或```标识

```markdown
    ```
    这里是代码
    ```
```

代码语法高亮在 ```后面加上空格和语言名称即可
 ```markdown 
    ``` 语言
    //注意语言前面有空格
    这里是代码
    ```
 ```

### 7 表格

表格对齐格式

居左：`:----`
居中：`:----:`或`-----`
居右：`----:`

```markdown
|标题|标题|标题|
|:---|:---:|---:|
|居左测试文本|居中测试文本|居右测试文本|
|居左测试文本1|居中测试文本2|居右测试文本3|
|居左测试文本11|居中测试文本22|居右测试文本33|
|居左测试文本111|居中测试文本222|居右测试文本333|
```

效果如下

|标题|标题|标题|
|:---|:---:|---:|
|居左测试文本|居中测试文本|居右测试文本|
|居左测试文本1|居中测试文本2|居右测试文本3|
|居左测试文本11|居中测试文本22|居右测试文本33|
|居左测试文本111|居中测试文本222|居右测试文本333|

### 8 分隔线

在一行中用三个以上的 `*` 、 `-` 、 `_` 来建立一个分隔线，行内不能有其他东西。也可以在符号间插入空格

```markdown
***
---
___
* * *
```

### 9 换行

在行尾添加两个空格  
加回车表示换行


### 10 脚注（注解）

使用 `[^]` 来定义脚注

```markdown
这是一个脚注的例子[^1]

[^1]: 这里是脚注
```

这是一个脚注的例子[^1]


### 11 转义字符

在字符前加反斜杠 ` \ ` 即可

```
*
`
*
_
{}
()
#
+
-
.
!
```



### 11 常用弥补Markdown的Html标签

a) 字体

```markdown
<font face="微软雅黑" color="red" size="6">字体及字体颜色和大小</font>
<font color="#0000ff">字体颜色</font>
```

<font face="微软雅黑" color="red" size="6">字体及字体颜色和大小</font>
<font color="#0000ff">字体颜色</font>

b) 换行

使用html标签`<br/>`<br/>换行

c) 文本对齐方式

```markdown
<p align="left">居左文本</p>
<p align="center">居中文本</p>
<p align="right">居右文本</p>
```

<p align="left">居左文本</p>
<p align="center">居中文本</p>
<p align="right">居右文本</p>

d) 下划线

```markdown
<u>下划线文本</u>
```

<u>下划线文本</u>


> end of file