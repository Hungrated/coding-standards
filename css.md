# 层叠样式表

### 1 CSS选择器

#### 1.1 分类

1. 标签选择器(如：body, div, p, ul, li)

2. 类选择器(如：class="head", class="head_logo")

3. ID选择器(如：id="name", id="name_txt")

4. 全局选择器(如：*号)

5. 组合选择器(如：.head .head_logo, 注意两选择器用空格键分开)

6. 后代选择器(如：#head .nav ul li 从父集到子孙集的选择器)

7. 群组选择器 div, span, img {color:Red} 即具有相同样式的标签分组显示

8. 继承选择器(如：div p,注意两选择器用空格键分开)

9. 伪类选择器(如：就是链接样式, a元素的伪类，4种不同的状态：link、visited、active、hover。)

10. 字符串匹配的属性选择符(^ $ * 三种，分别对应开始、结尾、包含)

11. 子选择器 (如：div>p ,带大于号>)

12. CSS 相邻兄弟选择器器 (如：h1+p,带加号+)

#### 1.2 优先级

总体： `!important` > 行内样式 > id选择器 > 类选择器 > 标签 > 通配符 > 继承 > 浏览器默认属性

> * 内联样式表的权值为 1000
> * id 选择器的权值为 100
> * Class 类选择器的权值为 10
> * HTML 标签选择器的权值为 1

注意事项： 

!important的优先级是最高的，但出现冲突时则需比较”四位数“;
优先级相同时，则采用就近原则，选择最后出现的样式;
继承得来的属性，其优先级最低;

#### 1.3 简洁高效原则
所谓高效就是让浏览器查找更少的元素标签来确定匹配的style元素。

1. 不要再id选择器前使用标签名

解释：id选择是唯一的，加上标签名相当于画蛇添足了，没必要。

2.不要在类选择器前使用标签名

解释：如果没有相同的名字出现就是没必要，但是如果存在多个相同名字的类选择器则有必要添加标签名防止混淆，如 `p.colclass{color: red;}` 和 `span.colclass{color: red;}`

3.尽量少使用层级关系

`#divclass p.colclass{color: red;}` 改为 `.colclass{color: red;}`

4.使用类选择器代替层级关系（如上） 

### 2 布局解决方案

#### 2.1 水平居中

1. inline-block + text-align

* 原理：先将子框由块级元素改变为行内块元素，再通过设置行内块元素居中以达到水平居中。

* 用法：对子框设置display:inline-block，对父框设置text-align:center。

* 优点：兼容性好，甚至可以兼容ie6、ie7

* 缺点：child里的文字也会水平居中，可以在.child添加text-align:left;还原

2. table + margin

* 原理：先将子框设置为块级表格来显示（类似 <table>），再设置子框居中以达到水平居中。

* 用法：对子框设置display:table，再设置margin:0 auto。

* 优点：只设置了child，ie8以上都支持

* 缺点：不支持ie6、ie7,将div换成table

3. absolute + transform

* 原理：将子框设置为绝对定位，移动子框，使子框左侧距离相对框左侧边框的距离为相对框宽度的一半，再通过向左移动子框的一半宽度以达到水平居中。当然，在此之前，我们需要设置父框为相对定位，使父框成为子框的相对框。

* 用法：对父框设置position:relative，对子框设置position:absolute，left:50%，transform:translateX(-50%)。

* 优点：居中元素不会对其他的产生影响

* 缺点：transform属于css3内容，兼容性存在一定问题，高版本浏览器需要添加一些前缀

4. flex + margin

* 原理：通过CSS3中的布局利器flex将子框转换为flex item，再设置子框居中以达到居中。

* 用法：先将父框设置为display:flex，再设置子框margin:0 auto。

* 缺点：低版本浏览器(ie6 ie7 ie8)不支持

5. flex + justify-content

* 原理：通过CSS3中的布局利器flex中的justify-content属性来达到水平居中。

* 用法：先将父框设置为display:flex，再设置justify-content:center。

* 优点：设置parent即可

* 缺点：低版本浏览器(ie6 ie7 ie8)不支持

#### 2.2 垂直居中

1. table-cell + vertical-align

* 原理：通过将父框转化为一个表格单元格显示（类似 `td` 和 `th` 标签），再通过设置属性，使表格单元格内容垂直居中以达到垂直居中。

* 用法：先将父框设置为display:table-cell，再设置vertical-align:middle。

* 优点：兼容性较好，ie8以上均支持

2. absolute + transform

* 原理：类似于水平居中时的absolute+transform原理。将子框设置为绝对定位，移动子框，使子框上边距离相对框上边边框的距离为相对框高度的一半，再通过向上移动子框的一半高度以达到垂直居中。当然，在此之前，我们需要设置父框为相对定位，使父框成为子框的相对框。

* 用法：先将父框设置为position:relative，再设置子框position:absolute，top:50%，transform:translateY(-50%)。

* 优点：居中元素不会对其他的产生影响

* 缺点：transform属于css3内容，兼容性存在一定问题，高版本浏览器需要添加一些前缀

3. flex + align-items

* 原理：通过设置CSS3中的布局利器flex中的属性align-items，使子框垂直居中。

* 用法：先将父框设置为display:flex，再设置align-items:center。

* 优点：只设置parent

* 缺点：兼容性存在一定问题

#### 2.3 水平垂直居中

1. absolute + transform

* 原理：将水平居中时的absolute+transform和垂直居中时的absolute+transform相结合。详见：水平居中的3）和垂直居中的2）。

* 用法：见水平居中的3）和垂直居中的2）。

* 优点：child元素不会对其他元素产生影响

* 缺点：兼容性存在一定问题

2. inline-block + text-align + table-cell + vertical-align

* 原理：使用inline-block+text-align水平居中，再用table-cell+vertical-align垂直居中，将二者结合起来。详见：水平居中的1）和垂直居中的1）。

* 用法：水平居中的1）和垂直居中的1）。

* 优点：兼容性较好

3. flex + justify-content + align-items

* 原理：通过设置CSS3布局利器flex中的justify-content和align-items，从而达到水平垂直居中。详见：水平居中的4）和垂直居中的3）。

* 用法：见水平居中的4）和垂直居中的3）。

* 优点：只设置了parent

* 缺点：兼容性存在一定问题

#### 2.4 多列定宽与自适应

1. float + overflow

* 原理：通过将左边框脱离文本流，设置右边规定当内容溢出元素框时发生的事情以达到多列布局。

* 用法：先将左框设置为float:left、width、margin-left，再设置实际的右框overflow:hidden。

* 优点：简单

* 缺点：不支持ie6

2. float + margin

* 原理：通过将左框脱离文本流，加上右框向右移动一定的距离，以达到视觉上的多列布局。

* 用法：先将左框设置为float:left、margin-left，再设置右框margin-left。

* 优点：简单，易理解

* 缺点：兼容性存在一定问题，ie6下有3px的bug。right下的p清除浮动将产生bug

3. float + margin（改良版）

* 原理：在1）的基础之上，通过向右框添加一个父框，再加上设置左、右父框属性使之产生BFC以去除bug。

* 用法：先将左框设置为float:left、margin-left、position:relative，再设置右父框float:right、width:100%、margin-left，最后设置实际的右框margin-left。

* 优点：简单，易理解

4. table

* 原理：通过将父框设置为表格，将左右边框转化为类似于同一行的td，从而达到多列布局。

* 用法：先将父框设置为display:table、width:100%、table-layout:fixed，再设置左右框display:table-cell，最后设置左框width、padding-right。

5. flex

* 原理：通过设置CSS3布局利器flex中的flex属性以达到多列布局。

* 用法：先将父框设置为display:flex，再设置左框flex:1，最后设置左框width、margin-right。

* 优点：flex很强大

* 缺点：兼容性存在一定问题，性能存在一定问题

#### 2.5 两列定宽与一列自适应

* 原理：这种情况与两列定宽差不多。

* 用法：先将左、中框设置为float:left、width、margin-right，再设置右框overflow:hidden。

#### 2.5 不定宽与自适应

1. float + overflow

* 原理：这种情况与两列定宽差不多。

* 用法：先将左框设置为float:left、margin-right，再设置右框overflow: hidden，最后设置左框中的内容width。

* 优点：简单

* 缺点：ie6下兼容性存在一定问题

2. table

* 原理：通过将父框改变为表格，将左右框转换为类似于同一行的td以达到多列布局，设置父框宽度100%，给左框子元素一个固定宽度从而达到自适应。

* 用法：先将父框设置为display: table、width: 100%，再设置左、右框display: table-cell，最后设置左框width: 0.1%、padding-right以及左框中的内容width。

* 缺点：ie6 ie7不支持

3. flex

* 原理：通过设置CSS3布局利器flex中的flex属性以达到多列布局，加上给左框中的内容定宽、给右框设置flex达到不定款+自适应。

* 用法：先将父框设置为display:flex，再设置右框flex:1，最后设置左框margin-right:20px、左框中的内容width。

* 优点：flex很强大

* 缺点：兼容性存在一定问题，性能存在一定问题

#### 2.6 两列不定宽与一列自适应

* 原理：这个情况与一列不定宽+一列自适应差不多。

* 用法：先将左、中框设置为float:left、margin-right，再设置右框overflow:hidden，最后给左中框中的内容设置width。


**参考资料**：https://www.itcodemonkey.com/article/2848.html
