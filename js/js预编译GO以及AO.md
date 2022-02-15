# 预编译

js 运行，大致上可以分为三个步骤（有的地方分为四个）

1. 通篇语法分析 检查语法错误等 （词法分析 语法分析）
2. 预编译
3. 解释执行

编译一行，执行一行，但 ```js```并非上来就进入编译环节。

预编译一般有两种：全局的预编译和函数的预编译，分别发生在```script```内代码执行前和函数的执行前

**函数声明整体**提升，**变量只有声明**提升，赋值是不提升的

### 全局预编译

全局中不存在形参和实参，所以全局预编译只需处理变量声明和函数声明

1. 生成 ``` GO(Global Object)```
2. 找变量声明，由于全局变量默认挂载在 ``` window```之上，若 ``` window``` 当前已存在当前属性，忽略当前操作，若没有，变量作为属性名，值赋予 ```undefined```。
3. 找函数声明，函数与变量类似，先去 ```window ```上查看，不存在函数作为函数名，值为函数体（若存在，重新赋值函数体）

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

### 函数预编译

1. 预编译开始，会建立 ``` AO(Activation Object) ``` 对象 
2. 找形参和变量声明，使其作为 ```AO```的属性名，值赋予 ``` undefined ```
3. 实参和形参相统一（将实参值赋值给形参）
4. 找函数声明，函数名作为 ``` AO ```的属性名，值赋予函数体



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

- ```[[scope]]``` ：每个函数在创建时，都会有一个隐藏属性 ``` [[scope]]```,它指向创建该函数时的 ``` AO```
- AO 变量对象： 也可以称为 VO ，存储函数中所需要的变量，参数、函数等数据，其中包含一个额外的属性，该属性指向创建该AO的函数本身
- 作用域链：[[scope chain]] 中所存储的执行期上下文对象集合，这个集合呈链式链接，这种链式链接叫做作用域链
- 查找变量：在哪个函数里查找变量，就从那个函数大的作用域链顶端依次向下查找。

### JavaScript 中的作用域

- 全局作用域
- 局部作用域

````javascript
    function foo(){
      function bar(){
        var inner = 234;
        outer = 0;
        console.log(inner);
      }
      var outer = 123;
      bar();
      console.log(outer);
      console.log(glob);
    }
    var glob = 100;
    foo();
````



