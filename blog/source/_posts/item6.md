---
title: 解析url
tags: [javascript]
---

  ```
  http://www.domain.com/?user=anonymous&id=123&id=456&city=%E5%8C%97%E4%BA%AC&d&enabled
  ```
把上面的URL串解析成下面这个格式（用原生js）：
```
{
  user: 'anonymous',
  id: [123, 456],     // 重复出现的 key 要组装成数组，能被转成数字的就转成数字类型
  city: '北京',        // 中文
  enabled: true,      // 未指定值的 key 约定值为 true
}
```
使用 ES6 编写的参考代码如下：
``` javascript
function parse(str) {
 if(typeof str !== 'string') return {}
 return decodeURI(str).split('&').map(param => {
   const tmp = param.split('=')
   const key = tmp[0]
   let value = tmp[1] || true
   if(typeof value === 'string' && isNaN(Number(value)) === false) value = Number(value)
   return {key, value}
 }).reduce((pre, cur) => {
   const {key, value} = cur
   if (typeof pre[key] === 'undefined') pre[key] = value
   else {
     pre[key] = Array.isArray(pre[key]) ? pre[key] : [pre[key]]
     pre[key].push(value)
   }
   return pre
 }, {})
}
```