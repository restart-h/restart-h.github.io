---
title: JavaScript功能函数
date: 2018-11-20 10:36:00
tags:
  - JavaScript
  - 函数
categories:
  - JavaScript

---

### 判断数据类型
用 . 访问
```bash
Object.prototype.dataType = function (){
  let toStr = Object.prototype.toString.call(this);
  return `is ${toStr.slice(8,-1)}`
}
```
直接使用
```bash
function dataType (arg){
  let toStr = Object.prototype.toString.call(arg);
  return `is ${toStr.slice(8,-1)}`
}
dataType(); // "is Undefined"
dataType(null); // "is Null"
dataType(undefined); // "is Undefined"
dataType(1); // "is Number"
dataType(''); // "is String"
dataType([]); // "is Array"
dataType({}); // "is Object"
dataType(Object); // "is Function"
dataType(new Object()); // "is Object"
dataType(new Object); // "is Object"
dataType(new Set()); // "is Set"
dataType(new Map()); // "is Map"
dataType(Symbol()); // "is Symbol"
dataType(new RegExp); // "is RegExp"
```