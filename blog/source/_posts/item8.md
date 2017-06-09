---
title: js数组与字符串常用方法总结
tags: [javascript]
---

### string 常用方法
1. substring(start开始位置的索引,end结束位置索引) 
截取的位置不包含结束位置的字符,只写一个参数表示从开始位置截取到最后
输入负值时将负值变为0，哪个较小作为开始位置
```
var str='abcdefg'
str.substring(2) //cdefg
str.substring(1,3) //bc
str.substring(-1,1) =>str.substring(0,1) //a
str.substring(1,-2) =>str.substring(0,1) //a
```
2. substr(start开始位置索引,end需要返回的字符个数)
```
var str='abcdefg'
str.substr(2) //cdefg
str.substr(1,1) //b
```
3. slice(start开始位置索引，end结束位置索引)
基本和substring相似,
区别在参数为负数时:输入负值时 值与字符串的长度相加
```
var str='abcdefg' 
str.slice(2)  //cdefg
str.slic(1,3) // bc
str.slice(-1) =>str.slice(6)    //g
str.slice(1,-2) =>str.slice(1,5)  //bcde
```
4. charAt(index)
返回指定索引位置处的字符。如果超出有效范围(index从0开始)的索引值返回空字符串.
```
var str='abcdefg'
str.charAt(2) // c
```
5. indexOf(string)
返回String对象内第一次出现子字符串位置。如果没有找到子字符串，则返回-1。
```
var str='abcdefga'
str.indexOf('b')  // 1
str.indexOf('h') //-1
```
6. lastIndexOf(string)  
倒叙查找,返回String对象内第一次出现子字符串位置。如果没有找到子字符串，则返回-1。
```
var str='abcdefga'
str.lastIndexOf('a') // 7
```
7. split(param)
将字符串以参数分割为数组
```
var str='abcadeafg'
str.split('a') //["", "bc", "de", "fg"]
```
8. toLowerCase()
返回一个字符串，该字符串中的字母被转换成小写。
```
var str = 'ABCDEF'
str.toLowerCase()  // 'abcdef'
```
9. toUpperCase()
返回一个字符串，该字符串中的所有字母都被转换为大写字母。
```
var str = 'abcEF'
str.toUpperCase()  // 'ABCDEF'
```
10. match()
可在字符串内检索指定的值，或找到一个或多个正则表达式的匹配
```
var str = '1a2b3c4d5e'
console.log(str.match('h'))    //返回null
console.log(str.match('b'))    //返回["b", index: 3, input: "1a2b3c4d5e"]
console.log(str.match(/b/))    //返回["b", index: 3, input: "1a2b3c4d5e"]
```
11. search(regExp)
返回与正则表达式查找内容匹配的第一个字符串的位置。
```
var str = 'abcDEF';
console.log(str.search('c'))   //返回2
console.log(str.search('d'))   //返回-1
console.log(str.search(/d/i))  //返回3
```
12. replace(oldValue,newValue)
替换字符串中的元素，返回替换后的字符串,只会替换查找到的第一个元素，即便后面还有相同元素 （传多参数是会报错的哦）
```
var str = 'abcdef'
console.log(str.replace('d','t'))  // 'abctef'
console.log(str.replace('c'))      // 'abundefineddfe' 只传一个会用undefined替换查找到元素

var str = 'abcdeabcdeABCDE'
console.log(str.replace(/a/gi, '$'))   //返回$bcde$bcde$BCDE
```
13. trim()
去除两端的空格，不影响之前的字符串
```
var arr = '  abcdefg     '
var a = arr.trim()
console.log(a)    // 'abcdefg'
console.log(arr)  // '  abcdefg     '
```
14. concat(str)
连接字符串,原来的字符串不变，生成新的字符串。
```
var a = 'abc'
var b = a.concat('def')
console.log(a)  // 'abc'
console.log(b)  // 'abcdef'
```
### 数组常用的方法
示例： 
```
var arr = ['a','b','c']
```
1. push(item1,item2,item3...)
在数组的后面添加元素，一次可以传入多个参数.
元素会根据当前传入的顺序添加到数组的后面。
1、该方法会改变原数组 2、该方法自身会返回新数组的长度
```
var result = arr.push(9)
console.log(result)  // 4
console.log(arr)     // ['a','b','c'，9]

var result1 = arr.push(9,8,7)
console.log(result1)   // 7
console.log(arr)       // ['a','b','c',9,9,8,7]
```
2. unshift(item1,item2,item3...)
在数组的前面添加元素，一次可以传入多个参数。
注意：元素会根据当前传入的顺序添加到数组的前面。
1、该方法会改变原数组 2、该方法自身会返回新数组的长度
```
var result = arr.unshift(9)
console.log(result)  // 4
console.log(arr)     // [9,'a','b','c']

var result1 = arr.unshift(9,8,7)
console.log(result1)   // 7
console.log(arr)       // [9,8,7,9,'a','b','c']
```
3. shift()
删除数组中索引为0的元素,不接受传参（传参会被忽略）
1、该方法会改变原数
2、该方法自身会返回删除的元素（注意是元素哦，不是索引~）
3、若数组为空，该方法自身会返undefined
```
var result = arr.shift()
console.log(result)   // 'a'
console.log(arr)      // ['b','c']
```
4. pop()
删除数组中最后一个元素,不接受传参（传参会被忽略）
1、该方法会改变原数
2、该方法自身会返回删除的元素（注意是元素哦，不是索引~）
3、若数组为空，该方法自身会返undefined
```
var result = arr.pop()
console.log(result)  // 'c'
console.log(arr)     // ['a','b']
```
5. reverse()
翻转数组，改变原数组,
不接受参数（只要不传非法值，不会影响其功能）
```
var result = arr.reverse()
console.log(result)// ['c','b','a']
console.log(arr)// ['c','b','a']
```
6. join()
将数组转化为字符串，中间以传入的参数连接； 
注意：传入多个参数时，只会选取第一个参数，若不传参，默认以逗号连接。
1、该方法不会改变原数组
2、该方法返回以传入的参数连接的字符串形式的数组元素 
```
var result = arr.join('-')
console.log(result)// 'a-b-c'
console.log(arr)// ['a','b','c']
```
7. slice(start,end)
截取字符串片段，start与end都是索引值，截取的元素范围[start,end),包含start,不包含end
1、返回一个新数组，不会改变原数组
```
1、若不传参数，默认截取整个数组，返回新数组
var result = arr.slice()
console.log(result)// ['a','b','c']
console.log(arr)// ['a','b','c']

2、若传一个参数，表示从当前参数索引开始，截取到数组的最后一个元素
var result = arr.slice(2)
console.log(result)// ['c']
console.log(arr)// ['a','b','c']

3、若传一个负数，表示从数组中倒数这个数的位置，截取到数组的最后一个元素
var result = arr.slice(-2)
console.log(result)// ['b','c']
console.log(arr)// ['a','b','c']

4、传两个参数（若起始参数大于结束参数，会返回空数组）
var result = arr.slice(1,2)
console.log(result)// ['b']
console.log(arr)// ['a','b','c']

5、传两个参数，若前一个为正，后一个为负，则会从前一个的索引开始，截取到倒数负数个数的位置
var result = arr.slice(1,-1)
console.log(result)// ['b']
console.log(arr)// ['a','b','c']
```
8. toString()
将数组转化为字符串，中间以逗号连接。
1、该方法不会改变原数组
2、该方法返回以逗号连接的字符串形式的数组元素
```
var result = arr.toString()
console.log(result)  // 'a,b,c'
console.log(arr)     // ['a','b','c']
```
9. concat()
将两个数组进行连接，同时也可直接传入元素，若是不传参，可以进行数组的复制。
1、返回一个新数组，不会改变原数组
```
var result = arr.concat([1,2])
console.log(result)  // ['a','b','c',1,2] 传入的数组默认添加到元素的后面
console.log(arr)     // ['a','b','c']

var result = arr.concat(1,2)
console.log(result)  // ['a','b','c',1,2] 可以直接传入元素，并以逗号间隔
console.log(arr)     // ['a','b','c']

var result = arr.concat()
console.log(result)  // ['a','b','c'] 
console.log(arr)     // ['a','b','c']
```
10. splice(start,len,item，item...)
删除片段，start表示开始索引，len表示删除的个数，item为可选参数，表示删除后插入的元素(在删除的位置开始插入)
1、该方法会返回删除的元素，同时改变原数组
```
1、若不传参，则不删除，返回空数组

2、若传一个参数，则表示从当前参数索引的位置开始，删除到最后一个元素
var result = arr.splice(1)
console.log(result)  // ['b','c']
console.log(arr)    // ['a']

3、若传一个参数且为负数表示从倒数这个数开始，删除到最后一个元素
var result = arr.splice(-1)
console.log(result)  // ['c']
console.log(arr)    // ['a','b']

4、传两个参数时，若item为负数，则会返回一个空数组，相当于没有操作

5、传三个或以上的参数时，从第三元素开始，会被插入到被删除的元素的位置
var result = arr.splice(1,1,4,5)
console.log(result)// ["b"]
console.log(arr)// ["a", 4, 5, "c"]
```
11. indexOf(item,index)
item表示要查找的元素，index表示查找的起始索引值，
返回找到的元素的索引值
1、该方法会改变原数
```
1、找到后就会停止查找，即便后面还有这个元素
var result = arr.indexOf('a',0)
console.log(result) // 0
console.log(arr)   // ['a','b','c']

2、若没有找到，则会返回-1
var result = arr.indexOf('d',0)
console.log(result)  // -1

3、若index不传参，默认从索引为0的位置查找
var result = arr.indexOf('a')
console.log(result)  // 0

4、若index传负数，则从倒数这个数的位置开始向数组后面查找
var result = arr.indexOf('c',-2)
console.log(result)  // 2
```
12. lastIndexOf(item1,item2)
与indexOf一样，只不过是从后往前找
13. sort()
数组排序，默认从小到大,改变原数组
```
var arr = ['a','b','c'，1,2]
1、数字优先字母
var result = arr.sort()
console.log(result)// [1, 2, "a", "b", "c"]
console.log(arr)// [1, 2, "a", "b", "c"]

2、单词排序按首字母排序，若首字母相同则比较第二个字母，以此类推
var arr = ['ba','ce','bb','aa']
var result = arr.sort()
console.log(result)// ["aa", "ba", "bb", "ce"]
console.log(arr)// ["aa", "ba", "bb", "ce"]

3、多位数排序，同样从第一位开始比较，若相同则比较第二位，以此类推
var arr = ['33','1','123']
var result = arr.sort()
console.log(result)// ["1", "123", "33"]
console.log(arr)// ["1", "123", "33"]

若想真正实现大小排序，该方法接受固定的参数，Array.prototype.sort(function(a,b) {return a-b})
形参的顺序为a,b，return a-b 表示升序，b-a表示降序
var arr = ['33','1','123']
var result = arr.sort(function(a,b){return a-b})
console.log(result) // ["1", "33", "123"]
console.log(arr)    // ["1", "33", "123"]
```