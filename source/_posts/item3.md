---
title: 前端项目中如何使用iconfont
tags: [iconfont]
---

1.首先可以创建一个文件夹fonts，用来放以下iconfont的文件
```
fonts
  iconfont.eot
  iconfont.svg
  iconfont.ttf
  iconfont.woff
```
2.可以在专门放样式的文件夹（styles）里面创建一个icon.css的文件，里面放入：
```
@font-face {
  font-family: "iconfont";
  src: url('iconfont.eot'); /* IE9*/
  src: url('iconfont.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
  url('iconfont.woff') format('woff'), /* chrome、firefox */
  url('iconfont.ttf') format('truetype'), /* chrome、firefox、opera、Safari, Android, iOS 4.2+*/
  url('iconfont.svg#iconfont') format('svg'); /* iOS 4.1- */
}

[class^="icon-"], [class*=" icon-"] {
  /* use !important to prevent issues with browser extensions that change fonts */
  font-family: 'iconfont' !important;
  font-style: normal;
  font-weight: normal;
  font-variant: normal;
  text-transform: none;
  line-height: 1;
  vertical-align: middle;
  /* Better Font Rendering =========== */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.icon-wexin:before {
  content: "\e615";
}
```
3.记得在项目中要引入这个icon.css文件