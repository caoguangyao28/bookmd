# 预编译

js 运行，三个步骤

1. 通篇语法分析 检查语法错误等
2. 预编译过程
3. 解释一行执行一行

函数声明整体提升，变量只有声明提升，赋值是不提升的

```javascript
console.log(a);// 
function a(a){
	var a = 10;
	var a = function(){}
}
var a = 1;
console.log(a);
// GO = {
	a:underfined => function a(a)=>1
}

// 暗示全局变量 imply global variable 
// window 全局域
```



```javascript
var a = 1;
function a(){
  console.log(2);
}
console.log(a) // 输出 1 
// GO 1，找变量   2，找函数声明  3，执行

```



```javascript
console.log(a,b); // 输出 a 函数，undefined
function a(){
}
var b = function(){};


```





```javascript
//AO  activation object 活跃上下文
function test(a){    // ao={a:und=>2=>a(),b:und,d:d()}
  console.log(a);
  var a = 1;//
  console.log(a);
  function a(){}
  console.log(a);
  var b = function(){} // b=>und=>fn
  console.log(b);
  function d(){
    
  }
}
test(2);
// AO  1,形参 变量声明，2 实参传给形参，3，函数声明及赋值 4，执行

// 题目 
       a = 1;
       function test(e){
           function e(){}
           arguments[0] = 2;
           console.log(e);
           if(a){
               var b = 3;

           }
           var c;
           a = 4;
           var a;
           console.log(b);
           f = 4;
           console.log(c);
           console.log(a);
       }

       var a;
       test(1);
       console.log(a);
       console.log(f);


```



## 作用域 scope ，作用域链 scope chain 



