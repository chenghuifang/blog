---
title: 你必须要弄明白的几个js概念！
tags: [javascript]
---

### JavaScript数据类型
1.Number类型
   数值转换：
    Number()转型函数，可以用于任何数据类型；
    parseInt()，将值转换为整型，用的比较多；
    parseFloat()；将值转换为浮点型。
2.String类型
   字符串转换：
    String()转型函数,适用于任何数据类型（null,undefined转换后为null和undefined）；
    toString() （null,defined没有toString()方法）。
3.Boolean类型
   转换为boolean值:
    转型函数Boolean(),将某个值转换为Boolean类型。
4.Null类型
5.Undefined类型
6.Object类型

### typeof 运算符返回值
可能的字符串有："number"、"string"、"boolean"、"object"、"function" 和 "undefined"。(typeof null 返回的是object)
注意:类型返回值都是字符串、而且都是小写打头
     如果我们想要判断一个变量是否存在，可以使用typeof：(不能使用if(a) 若a未声明，则报错)
```
表达式 	          返回值
typeof undefined 	      'undefined'
typeof null 	          'object'
typeof true 	          'boolean'
typeof 123 	            'number'
typeof "abc" 	          'string'
typeof function() {} 	  'function'
typeof {} 	            'object'
typeof [] 	            'object'
typeof unknownVariable 	'undefined'
```
### instanceof
 instanceof用于判断一个动态的变量是否是某个对象的实例，instanceof返回的是一个布尔值。
 ```
var b = '123'
alert(b instanceof String)  //false
alert(typeof b)  //string

var c = new String("123")
alert(c instanceof String)  //true
alert(typeof c)  //object
 ```