#### live制作过程中stack
1. css中:active伪类在safari中不起作用的解决方案：
```html
<body ontouchstart="">
    ...
</body>
```
2. 通过:active伪类切换背景图片时出现闪动（active时才加载造成）解决方案：
提前预加载：
```js
::after{
 display:none;
 content: url(path/images/x.png) url(path/images/xx.png) url(path/images/xxx.png);
}
```
