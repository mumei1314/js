## let 和 const命令

ES6不再推荐使用var，无须担心语法兼容，有打包工具可以编译成ES5。

#### 1. let

和es5的var一样是声明变量用的，但是和es5的区别有：

- let不存在变量提升
- let不可以同一变量重复定义
- 暂时性死区TDZ--如果当前作用域let了某一变量，那在这之前是不允许使用该变量的，即使外面作用域有

*以下情况都会报错：*

```js
//1
console.log( a );
let a = 10;

//2
let a = 10;
let a = 20;

//3
var a = 10;
let a = 20;

//4
function g(a){
    let a = 10;
}

//5
let a = 10;
function g(){
    alert(a);
    let a = 20;
}
```

#### 2. const

const（*常量*）和let一样也是定义变量的，保持let的特性，不同于let的有：

- const声明的变量必须立马赋值
- const声明的变量不允许再次重新赋值

*以下情况都会报错：*

```js
//1
const a;

//2
const a = 1;
a = 2;
```

*以下情况不会报错：*

```js
//1
const arr = [];
arr.push(1);

//2
const a = {};
a.x = 10;
```

#### 3.块级作用域

let和const在某些语法里面会变量有块级作用域的特性。

- {  } 作用域 for() 里的特殊情况

```js
//1
{
    var a = 10;
    let b = 20;
}
alert(a); //10
alert(b); //报错  b is not defined

//2
if(true)
{
    var a = 10;
    let b = 20;
}
alert(a); //10
alert(b); //报错  b is not defined

//3
for(var i=0;i<5;i++){
    var x = 10;
}
alert(i); //5
alert(x); //10
for(let j=0;j<5;j++){
    let y = 10;
}
	// alert(i); // 报错 -- i is not defined
alert(y); //报错 -- y is not defined
```

- 块级作用域嵌套

```js
{
    {
        let a = 10;
    }
    alert(a); //报错
}
```

- es5与es6 在if判断语句里面使用function关键字声明变量时都有很奇怪的表现，比如ES5明确禁止在if语句里面使用function，但是实际上确为了保证兼容能够使用。**所以无论什么情况，都不要在if语句里面使用function来声明变量**。

#### 4. 顶层对象

全局下，let const声明的变量不再属于window

```js
var a = 10;
let b = 20;

console.log( window.a ); // 10
console.log( window.b ); //undeinfed
```