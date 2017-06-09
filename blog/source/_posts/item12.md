---
title: 获取页面元素的位置
tags: [javascript]
---

####  clientHeight和clientWidth
这两个属性指元素的内容部分再加上padding的所占据的视觉面积，不包括border和滚动条占用的空间。
clientHeight = content + padding-top + padding-bottom
clientWidth = content + padding-left + padding-right
document元素的clientHeight和clientWidth属性，就代表了网页的大小。
```
   function getViewport() { //返回浏览器窗口的高和宽
　　　　if (document.compatMode == "BackCompat"){
　　　　　　return {
　　　　　　　　width: document.body.clientWidth,
　　　　　　　　height: document.body.clientHeight
　　　　　　}
　　　　} else {
　　　　　　return {
　　　　　　　　width: document.documentElement.clientWidth,
　　　　　　　　height: document.documentElement.clientHeight
　　　　　　}
　　　　}
　　}
```
注意：
    1）这个函数必须在页面加载完成后才能运行，否则document对象还没生成，浏览器会报错。

    2）大多数情况下，都是document.documentElement.clientWidth返回正确值。但是，在IE6的quirks模式中，document.body.clientWidth返回正确的值，因此函数中加入了对文档模式的判断。

    3）clientWidth和clientHeight都是只读属性，不能对它们赋值。
#### scrollHeight和scrollWidth
网页上的每个元素还有scrollHeight和scrollWidth属性，指包含滚动条在内的该元素的视觉面积。
#### offsetHeight和offsetWidth
offsetHeight = content + padding-top + padding-bottom + border-top + border-bottom
clientWidth = content + padding-left + padding-right + border-left + border-right

