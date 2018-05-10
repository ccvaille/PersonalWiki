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

## css 变量
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
## BFC
