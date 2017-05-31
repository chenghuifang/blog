---
title: 前端项目常用的转换方法
---

1.数组转化成MAP
``` javascript
function arr2map (arr, key) {
  return arr.reduce((prv, cur) => {
    prv[cur[key]] = cur
    return prv
  }, {})
}
```

2.MAP转化成数组
``` javascript
function map2arr (map) {
  return Object.keys(map).map(key => map[key])
}
```

3.回到顶部
``` javascript
function go2top () {
  let el = document.querySelector('.main')
  el.scrollTop = 0
}
```

4.过滤一个对象中为空字符串或者为null的属性
``` javascript
function filterObj(obj) {
  return Object.keys(obj).reduce((pre, cur) => {
    if (obj[cur] !== '' && obj[cur] !== null) {
      pre[cur] = obj[cur]
    }
    return pre
  }, {})
}
```