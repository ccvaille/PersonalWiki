## CSS3 新增选择器
- nth-child(n)
    - `nth(4n+1)` 隔三个选一个
- nth-last-child(n)
- nth-of-type(n)
    - 只关注同类标签
- nth-last-type(n)
- last-child
- first-child
- only-child
    - 唯一子元素
- only-of-type
- not(s)
    - `#foo:not(#bar)`

## 超出当行隐藏[ DEMO](../demos/css/超出隐藏.html)
```css
.overflow-hidden {
    display: block;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    width: 180px;
}
```
## 超出三行隐藏[ DEMO](../demos/css/超出隐藏.html)
```css
div {
    display: -webkit-box;
    overflow: hidden;
    text-overflow: ellipsis;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 3;
}
```

## calc[ DEMO](../demos/css/calc.html)

## CSS 变量
- `--` 声明变量
- `var()` 读取变量
    - 第二个参数为变量的默认值
- 提供了 JS 和 CSS 通信的一种途径
    - getPropertyValue() 读取变量
    - setProperty() 设置变量
    - removeProperty() 删除变量
```css
:root {
    --root-color: pink;
}
a {
    color: var(--root-color)；
}
```
## BFC（Block Formatting Context）
- 外边距折叠（Margin collapsing）也只会发生在属于同一BFC的块级元素之间。
- 根元素或包含根元素的元素
- 浮动元素（元素的 float 不是 none）
- 绝对定位元素（元素的 position 为 absolute 或 fixed）
- 行内块元素（元素的 display 为 inline-block）
- 表格单元格（元素的 display为 table-cell，HTML表格单元格默认为该值）
- 表格标题（元素的 display 为 table-caption，HTML表格标题默认为该值）
- 匿名表格单元格元素（元素的 display为 table、table-row、 table-row-group、table-header-group、table-footer-group（分别是HTML table、row、tbody、thead、tfoot的默认属性）或 inline-table）
- overflow 值不为 visible 的块元素
- display 值为 flow-root 的元素
- contain 值为 layout、content或 strict 的元素
- 弹性元素（display为 flex 或 inline-flex元素的直接子元素）
- 网格元素（display为 grid 或 inline-grid 元素的直接子元素）

## 六种垂直居中
- 父相对，子绝对，left 50% ,top 50% , margin-top: height/2. margin-left: width/2 [ DEMO](./demos/css/vertical-box1.html)
- 父相对，子绝对，left 0, right 0, top 0, bottom: 0, margin: auto [ DEMO](./demos/css/vertical-box2.html)
- 父相对，子绝对，left 50% ,top 50% ,transform: translate(-50%, -50%)[ DEMO](./demos/css/vertical-box3.html)
- 父 flex 子 margin auto[ DEMO](./demos/css/vertical-box4.html)
- 父 flex, justify-content: center, align-items: center,[ DEMO](./demos/css/vertical-box5.html)
- 父 table-cell, vertical-align: middle, text-align: center, 子 display： inline-block[ DEMO](./demos/css/vertical-box6.html)

## 响应式页面开发[ Responsive Web Design Basic](https://developers.google.com/web/fundamentals/design-and-ux/responsive/)
- 添加 viewport meta 标签(优化在移动设备上的展示效果)
```html
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
```
- Media Queries(为不同特性的浏览器视窗使用不同的样式代码)
```css
@media screen and (min-width: 640px) and (max-width: 1024px) {
    ...
}
```
- 使用 Viewport 单位及 rem(让页面元素的尺寸能够依据浏览器视窗尺寸变化而平滑变化)

## CSS Frameworks
- Bootstrap	1,768	34.69%
- Foundation	199	3.90%
- Materialize	134	2.63%
- Bulma	132	2.59%
- Semantic UI	102	2.00%
- PureCSS	33	0.65%
