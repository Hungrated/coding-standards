# SASS 语法规范

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

### 1.3 属性嵌套

有些 CSS 属性遵循相同的命名空间 (namespace)，比如 `font-family`, `font-size`, `font-weight` 都以 `font` 作为属性的命名空间。为了便于管理这样的属性，同时也为了避免了重复输入，Sass 允许将属性嵌套在命名空间中