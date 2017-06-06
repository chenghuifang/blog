---
title: 闭包---神奇的存在
tags: [javascript]
---

#### 举个例子
```
function makeFunc() {
  var name = "Mozilla";
  function displayName() {
    alert(name);
  }
  return displayName;
}

var myFunc = makeFunc();
myFunc();
```


