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
## 什么时候会创建 BFC（Block Formatting Context）
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

## BFC 的影响
- 浮动定位和清除浮动时只会应用于同一个BFC内的元素
- 浮动不会影响其它BFC中元素的布局，而清除浮动只能清除同一BFC中在它前面的元素的浮动
- 外边距折叠（Margin collapsing）也只会发生在属于同一BFC的块级元素之间。

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
```html
<link rel="stylesheet" media="screen and (min-width:500px)" hre="over500.css">
```
```css
@media screen and (min-width: 640px) and (max-width: 1024px) {
    ...
}
```

- 使用 rem(让页面元素的尺寸能够依据浏览器视窗尺寸变化而平滑变化)
    - rem 弹性布局的核心在于根据视窗大小变化动态改变根元素的字体大小
    - 给根元素的字体大小设置随着视窗变化而变化的 vw 单位，这样就可以实现动态改变其大小
        - 1vw 等于视口宽度的1%
    - 其他元素的文本字号大小、布局高宽、间距、留白都使用 rem 单位
    - 限制根元素字体大小的最大最小值，配合 body 加上最大宽度和最小宽度，实现布局宽度的最大最小限制
    - [DEMO](https://link.juejin.im/?target=https%3A%2F%2Fjdc.jd.com%2Fdemo%2Fting%2Fvw_rem_layout.html)
```css
// rem 单位换算：定为 75px 只是方便运算，750px-75px、640-64px、1080px-108px，如此类推
$vw_fontsize: 75; // iPhone 6尺寸的根元素大小基准值
@function rem($px) {
     @return ($px / $vw_fontsize ) * 1rem;
}
// 根元素大小使用 vw 单位
$vw_design: 750;
html {
    font-size: ($vw_fontsize / ($vw_design / 2)) * 100vw; 
    // 同时，通过Media Queries 限制根元素最大最小值
    @media screen and (max-width: 320px) {
        font-size: 64px;
    }
    @media screen and (min-width: 540px) {
        font-size: 108px;
    }
}
// body 也增加最大最小宽度限制，避免默认100%宽度的 block 元素跟随 body 而过大过小
body {
    max-width: 540px;
    min-width: 320px;
}
```
- 对于需要保持高宽比的图，应改用 padding-top 实现
```css
.mod_banner {
    position: relative;
    padding-top: percentage(100/750); // 使用padding-top
    height: 0;
    overflow: hidden;
    img {
        width: 100%;
        height: auto;
        position: absolute;
        left: 0;
        top: 0; 
    }
}
```

- [Google_Response_columnDrop_Demo](../Demos/css/response/columnDrop.html)
- [Google_Response_layoutShifter_Demo](../Demos/css/response/layoutShifter.html)
- [Google_Response_mostlyFluid_Demo](../Demos/css/response/mostlyFluid.html)
- [Google_Response_offCanvas_Demo](../Demos/css/response/offCanvas.html)
- [Google_Response_responseTable_Demo](../Demos/css/response/responseTable.html)
## 1 物理像素线（也就是普通屏幕下 1px ，高清屏幕下 0.5px 的情况）
- **scale**
```css
.hr.scale-half {
    height: 1px;
    transform: scaleY(0.5);
}
```
- box-shadow
```css
.hr.boxshadow {
    height: 1px;
    background: none;
    box-shadow: 0 0.5px 0 #000;
}
```
- linear-gradient
```css
.hr.gradient {
    height: 1px;
    background: linear-gradient(0deg, #fff, #000);
}
```
- SVG
```css
.hr.svg {
    background: none;
    height: 1px;
    background: url("data:image/svg+xml;utf-8,<svg xmlns='http://www.w3.org/2000/svg' width='100%' height='1px'><line x1='0' y1='0' x2='100%' y2='0' stroke='#000'></line></svg>");
}
```
- `<meta name="viewport" content="width=device-width,initial-sacle=0.5">`
## CSS Frameworks
- Bootstrap	1,768	34.69%
- Foundation	199	3.90%
- Materialize	134	2.63%
- Bulma	132	2.59%
- Semantic UI	102	2.00%
- PureCSS	33	0.65%
