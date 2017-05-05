# let和const命令
## let命令
ES6新增了let命令，用来声明变量。它的用法类似于var，但是所声明的变量，只在let命令所在的代码块内有效。
```javascript
{
    let a = 10;
    var b = 1;
}
a // ReferenceError: a is not defined.
b //1
```
for循环的计数器，就很合适使用let命令。
```javascript
var a = [];
for (var i = 0; i < 10; i++) {
  let c = i;
  a[i] = function () {
    console.log(c);
  };
}
a[6](); // 6
```
上面代码的计数器i，只在for循环体内有效。let不像var那样，会发生“变量提升”现象。

注意：ES5: Javascript没有块级作用域，块级作用域的意思是由花括号封闭的代码块都有自己的作用域。Javascript里是通过执行环境来区别全局和局部变量，每个函数都有自己的执行环境。     
ES6: let实际上为JavaScript新增了块级作用域。   

**立即执行匿名函数（IIFE）不需要**      

块级作用域的出现，实际上使得获得广泛应用的立即执行匿名函数（IIFE）不再必要了。
```javascript
// IIFE写法
(function () {
    var tmp = ...;
    ...
}());

// 块级作用域写法
{
    let tmp = ...;
    ...
}
```    

**函数提升改变**      

ES6也规定，函数本身的作用域，在其所在的块级作用域之内。
```javascript
function f() { console.log('I am outside!'); }
(function () {
  if(false) {
    // 重复声明一次函数f
    function f() { console.log('I am inside!'); }
  }

  f();
}());
```
上面代码在ES5中运行，会得到“I am inside!”，但是在ES6中运行，会得到“I am outside!”。这是因为ES5存在函数提升，不管会不会进入if代码块，函数声明都会提升到当前作用域的顶部，得到执行；而ES6支持块级作用域，不管会不会进入if代码块，其内部声明的函数皆不会影响到作用域的外部。

需要注意的是，如果在严格模式下，函数只能在顶层作用域和函数内声明，其他情况（比如if代码块、循环代码块）的声明都会报错。
## const命令
const也用来声明常量。一旦声明，常量的值就不能改变。
```javascript
const PI = 3.1415;
PI // 3.1415

PI = 3;
PI // 3.1415

const PI = 3.1;
PI // 3.1415
```
注意：    
1.对常量重新赋值不会报错，只会默默地失败。     

2.const的作用域与let命令相同：只在声明所在的块级作用域内有效。
```javascript
if (condition) {
    const MAX = 5;
}
// 常量MAX在此处不可得
```
3.const声明的常量，也与let一样不可重复声明。

Javascript全局变量和局部变量的陷阱：
http://www.imooc.com/article/5255
