# SASS 语法规范

> Sass 是一款强化 CSS 的辅助工具，它在 CSS 语法的基础上增加了变量 (variables)、嵌套 (nested rules)、混合 (mixins)、导入 (inline imports) 等高级功能，这些拓展令 CSS 更加强大与优雅。使用 Sass 以及 Sass 的样式库（如 Compass）有助于更好地组织管理样式文件，以及更高效地开发项目

### 1 CSS功能拓展

#### 1.1 嵌套规则

Sass 允许将一套 CSS 样式嵌套进另一套样式中，内层的样式将它外层的选择器作为父选择器

```scss
#main p {
  color: #00ff00;
  width: 97%;

  .box {
    background-color: #ff0000;
    color: #000000;
  }
}
```
> 嵌套功能避免了重复输入父选择器，而且令复杂的 CSS 结构更易于管理

#### 1.2 父选择器 `&`

在嵌套 CSS 规则时，有时也需要直接使用嵌套外层的父选择器，例如，当给某个元素设定 hover 样式时，或者当 body 元素有某个 classname 时，可以用 `&` 代表嵌套规则外层的父选择器

```scss
#main {
  color: black;
  a {
    font-weight: bold;
    &:hover { color: red; }
  }
}
```

> 编译后的 CSS 文件中 `&` 将被替换成嵌套外层的父选择器，如果含有多层嵌套，最外层的父选择器会一层一层向下传递

`&` 必须作为选择器的第一个字符，其后可以跟随后缀生成复合的选择器

```scss
#main {
  color: black;
  &-sidebar { border: 1px solid; }
}
```

#### 1.3 属性嵌套

有些 CSS 属性遵循相同的命名空间 (namespace)，比如 `font-family`, `font-size`, `font-weight` 都以 `font` 作为属性的命名空间。为了便于管理这样的属性，同时也为了避免了重复输入，Sass 允许将属性嵌套在命名空间中

```scss
.funky {
  font: {
    family: fantasy;
    size: 30em;
    weight: bold;
  }
}
```

#### 1.4 占位符选择器 `%foo`

Sass 额外提供了一种特殊类型的选择器：占位符选择器 (placeholder selector)。与常用的 id 与 class 选择器写法相似，只是 # 或 . 替换成了 %。必须通过 @extend 指令调用，更多介绍请查阅 @extend-Only Selectors

> 当占位符选择器单独使用时（未通过 `@extend` 调用），不会编译到 CSS 文件中

### 2 注释 `/* */` 与 `//`

Sass 支持标准的 CSS 多行注释 `/* */`，以及单行注释 `//`，前者会被完整输出到编译后的 CSS 文件中，而后者则不会

```scss
/* This comment is
 * several lines long.
 * since it uses the CSS comment syntax,
 * it will appear in the CSS output. */
body { color: black; }

// These comments are only one line long each.
// They won't appear in the CSS output,
// since they use the single-line comment syntax.
a { color: green; }
```

> 将 `!` 作为多行注释的第一个字符表示在压缩输出模式下保留这条注释并输出到 CSS 文件中，通常用于添加版权信息

参考：https://www.sass.hk/docs
