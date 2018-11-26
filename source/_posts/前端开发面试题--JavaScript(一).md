---
title: 前端开发面试题--JavaScript(一)
date: 2018-11-12 18:47:45
tags:
  - JavaScript
  - 面试题
  - ES6
categories: 
  - 面试题
  - JavaScript
  - ES6
---
> 以下内容来自：https://www.cnblogs.com/fengxiongZz/p/8191503.html
### ES6
#### 箭头函数
  当要求`动态上下文`的时候，就不能够使用箭头函数，也就是   this 的固定化

  1. 在使用 `()=>{}` 定义函数的时候，this 的指向是`定义时`所在的对象，而不是使用时所在的对象
  2. 不能够用作构造函数，即不能够使用 `new` 命令，否则就会抛出一个错误
  3. 不能够使用 `arguments` 对象
  4. 不能使用 `yield` 命令 

ex:
不使用箭头函数: 
```bash
class Boys{
  constructor(){
	  this.type='Tom';
	}
  say(val){
      setTimeout(function(){
	    console.log(this);
	    console.log(this.type + " says " + val)
    },1000)
  }
}
var boy = new Boys();
boy.say('hello'); // undefined says hello
```
  Tips: 超时调用的代码都是在全局作用域中执行的, 因此函数中`this` 的值在非严格模式下指向 window 对象, 在严格模式下是 undefined. 也就是说在非严格模式下, setTimeout 中所执行函数中的 this, 永远指向 window
使用 ()=>{}
```bash
class Girls{
  constructor(){
    this.type='Lucy';
	}
  say(val){
      setTimeout(()=>{
      console.log(this);
      console.log(this.type + " says " + val)
    },1000)
  }
}
var girl = new Girls();
girl.say('hai'); // Lucy says hai
```

#### let和const
  `let` 是更完美的 var，不是全局变量，具有块级函数作用域,大多数情况不会发生`变量提升`。
  `const` 定义常量值，不能够重新赋值，如果值是一个对象，可以改变对象里边的属性值。
  1. let 声明的变量具有块级作用域
  2. let 声明的变量不能通过 window. 变量名进行访问
  3. 形如 for(let x..) 的循环是每次迭代都为 x 创建新的绑定
var 带来的不合理场景
```bash
var arr = [];
for (var i = 0; i < 10; i++ ){
  arr[i] = function(){
    console.log(i)
  }
}
arr[3]() // 10
```
上述代码中, 变量 i 是 var 声明的, 在`全局范围`内都有效, 所以用来计数的循环变量`泄露`为全局变量. 所以每一次循环, 新的i值都会`覆盖旧值`, 导致最后输出都是10
```bash
var arr2 = [];
for (let i = 0; i < 10; i++){
  arr[i] = function (){
    console.log(i)
  } 
}
arr[3]() // 3
```
相当于简化闭包：
```bash
function exportNum(i){
  return function (){
    console.log(i)
  }
}
var a = [];
for ( var i = 0; i < 5; i++ ){
  a[i] = exportNum(i)();
}
// 循环输出 0, 1, 2, 3, 4
```
采用立即执行函数的闭包
```bash
var a = [];
for ( var i = 0; i < 5; i++ ){
  a[i] = (function (val){
    return function (){
      console.log(val)
    }
  }(i));
}
a[3](); // 3
```
#### Set 数据结构
ES6 方法, Set 本身是一个构造函数, 类似于数组, 但`成员值唯一`
```bash
const set = new Set([1,1,2,3,5,2,4])
undefined
console.log(...set) // 1 2 3 5 4
console.log(Array.from(new Set([2,2,3,3,5,7,7,9]))) //[2, 3, 5, 7, 9]
```
#### Class 语法
class 语法相对`原型`, `构造函数`, `继承`更接近传统语法, 它的写法能够让对象原型的写法更加`清晰`, 更加`通俗`
ex:
```bash
class Animal{
  constructor(){
    this.type='Lucy';
	}
  say(val){
      setTimeout(()=>{
      console.log(this);
      console.log(this.type + " says " + val)
    },1000)
  }
}
let animal = new Animal();
animal.say('hai'); // Lucy says hai

class Cat extends Animal {
  constructor(){
    super()
    this.type = "cat";
  }
}
let cat = new Cat();
cat.say('hai'); //cat says hai
```
使用 `extend` 的时候结构输出是 cat says hello 而不是animal says hello, 说明 `contructor` 内部定义的方法和属性是实例对象自己的, 不能通过 `extends` 进行继承;
在 class cat 中出现了 `super()`, 是因为在 ES6 中，子类的构造函数必须含有 super 函数, super 表示的是调用父类的构造函数, 虽然是父类的构造函数, 但是 this 指向的却是 cat 

#### 模板字符串
${ varible }, 以往连接字符串和变量的时候需要使用字符串拼接 `'string' + varible + 'string'` 但是有了模版语言后我们可以使用 string${varible}string 进行`简化`
```bash
//es5 
var name = 'Tom';
console.log('hello ' + name); // hello Tom

var tem = 'hello \
world'; 
console.log(tem); // hello world

//es6
const name = 'Tom';
console.log(`hello ${name}`); //hello Tom

const tem = `hello
world`;
console.log(tem); // hello 换行 world
```

