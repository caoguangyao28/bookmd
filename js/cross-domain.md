# 常见的跨域手段

## jsonp 方式

拥有src属性的html便签都可以加载不同域的文件 

jsonp 利用的是 script 标签 src 加载能力并且可以立即执行的特性。动态创建，加载脚本文件执行，达到跨域目的。即后端返回其实是函数执行

示列：

1,html  jsonp 利用的是src ，所以只有get方式。参数传递都是拼接 字符串 

代码中采用动态创建回调函数名称且定义全局函数，函数名作为参数 传到后端，后端接收后拼接执行语句返回给前端

前端收到响应后直接执行，执行后会删除动态创建script 便签引入，以及发起时创建的全局函数（为了安全）

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>jsonp</title>
  <!-- 只支持 get 方式  -->
  <script>
   var jsonp = function (url, data) {
      return new Promise((resolve, reject) => {
        // 初始化url
        let dataString = url.indexOf('?') === -1 ? '?' : '&'
        let callbackName = `jsonpCB_${Date.now()}`
        url += `${dataString}callback=${callbackName}`
        if (data) {
          // 有请求参数，依次添加到url
          for (let k in data) {
            url += `&${k}=${data[k]}`
          }
        }
        let jsNode = document.createElement('script')
        jsNode.src = url
        // 触发callback，触发后删除js标签和绑定在window上的callback
        window[callbackName] = result => {
          delete window[callbackName]
          var	valueC =  'test-token' + "=" + 'oj0ii9i3i9' + ";path=/";
          window.document.cookie = valueC;
          document.body.removeChild(jsNode)
          if (result) {
            resolve(result)
          } else {
            reject('没有返回数据')
          }
        }
        // js加载异常的情况
        jsNode.addEventListener('error', () => {
          delete window[callbackName]
          document.body.removeChild(jsNode)
          reject('JavaScript资源加载失败')
        }, false)
        // 添加js节点到document上时，开始请求
        document.body.appendChild(jsNode)
      })
    }
  </script>
</head>
<body>
  <script>
    jsonp('http://localhost:3000/say', { a: 1, b: 'heiheihei' }).then(result => { console.log(result) }).catch(err => { console.error(err) })
  </script>
</body>
</html>
```

2, server.js  本地服务端 使用的是node express 搭建的简易

用node 启动即可，node  ../../server.js

```js
const express =  require("express");
let app = express()
// 以文件所在目录作为 服务目录
app.use(express.static(__dirname));
// 响应 get 方式，hostname:port/say 请求
app.get('/say',function( req, res){
  let { a,callback } = req.query;
  console.log(a,callback);
  // req.cookies
  res.setHeader("JSESSIONID",'TEST')
  res.end(`${callback}('token:ddddfdd')`);
})
// 服务监听端口
app.listen(3000);
```



## domain + iframe 方式

主域名相同，子域名不同，列如： www.domain.com  child.domain.com 

实现原理：两个页面都通过js强制设置document.domain为基础主域，就实现了同域。

1, 主域下页面 a.html (局部主要代码)

```html
// 使用 iframe 载入 子域名下 b 页面 且 设置 当前页面 document.domain = 'domain.com'
<iframe id="iframe" src="http://child.domain.com/b.html"></iframe>
<script>
    document.domain = 'domain.com';
    var user = 'admin';
</script>
```

2, 子域下 b.html (局部主要代码)

```html
<script>
    // 通用设置 页面所在的 domain 为 ’domian.com‘
    document.domain = 'domain.com';
    // 获取父窗口中变量
    alert('get js data from parent ---> ' + window.parent.user);
</script>
```



## location.hash + iframe 方式





## window.name + iframe 方式



##  postMessage跨域（iframe）

postMessage是HTML5 XMLHttpRequest Level 2中的API，且是为数不多可以跨域操作的window属性之一，它可用于解决以下方面的问题：
a.） 页面和其打开的新窗口的数据传递 （window.open 方式原窗口可以标识）
b.） 多窗口之间消息传递 (如何获取到每个窗口?)
c.） 页面与嵌套的iframe消息传递
d.） 上面三个场景的跨域数据传递

Demo: c

1, localhost:3000

```js
// server.js 进入文件所在目录  node server.js 运行本地服务
const express =  require("express");
let app = express()
app.use(express.static(__dirname));
app.listen(3000);

```

2, localhost:3000/a.html （a.html 与 server.js 同目录）

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  AAAA
  <iframe style="display: none;" id="frame" src="http://localhost:4000/b.html" frameborder="0" onload="load()">
  </iframe>
  <script>
    // 访问localhost:3000/a.html 时 需要 先启动 localhost:4000 服务
    var	valueC =  'token' + "=" + 'oj0ii9i3i9' + ";path=/;";
    window.document.cookie = valueC;
    function load(){
      var frame = document.getElementById('frame');
      frame.contentWindow.postMessage(valueC,'http://localhost:4000');
      // 开启信息监听
      window.onmessage = function(e){
        console.log(e.data);
      }
    }
  </script>
</body>
</html>
```

3， localhost:4000 

```js
// server2.js 进入文件所在目录 node server2.js
const express =  require("express");
let app = express()
app.use(express.static(__dirname));
app.listen(4000);
```

4, localhost:4000/b.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  BBBB
  <script>
    // var	valueC =  'token' + "=" + 'oj0ii9i3i9i9i9494959jij' + ";path=/;";
    // window.document.cookie = valueC;

    window.onmessage = function(e){
      console.log(e.data);
      // window.document.cookie = e.data;
      // var v = decodeURIComponent(window.document.cookie).match('(^|;) ?' + 'token' + '=([^;]*)(;|$)');
      // var ret = v ? v[2] : null;
      // console.log(top);
      // console.log(window.parent);
      e.source.postMessage('from b.html ret',e.origin);
    }
  </script>
</body>
</html>
```





##  跨域资源共享cross 跨域

普通跨域请求：只服务端设置Access-Control-Allow-Origin即可，前端无须设置，若要带cookie请求：前后端都需要设置。

1 html 运行在 localhost:3000 下，访问 localhost:4000 下接口

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>cros</title>
</head>
<body>
  <script>
    document.cookie = 'name=chg';
    function createHttp(url,jsessionid){
      let xhr = new XMLHttpRequest();
      // 带上cookie 凭证
      xhr.withCredentials = true;
      xhr.open('GET',url,false);
      if(jsessionid){
        xhr.setRequestHeader('JSESSIONID',jsessionid);
      }

      xhr.onreadystatechange = function(){
        if(xhr.readyState === 4){
          if(xhr.status >= 200 && xhr.status < 300 || xhr.status === 304){
            console.log(xhr.response);
            console.log(xhr.getResponseHeader('JSESSIONID'));
          }
        }
      }
      xhr.send();
    }

    createHttp('http://localhost:4000/getData');

    // createHttp('http://localhost:4000/getMore','add');

  </script>
</body>
</html>
```

2， localhost:3000 的服务端 

```js
const express =  require("express");
let app = express()
app.use(express.static(__dirname));
app.listen(3000);
```

3, localhost:4000 的服务端

```js
const express =  require("express");
let app = express()
let whitelist = ['http://localhost:3000']

app.use(function(req,res,next){
  let origin = req.headers.origin;
  if(whitelist.includes(origin)){
    res.setHeader('Access-Control-Allow-Origin',origin);
    res.setHeader('Access-Control-Allow-Headers','JSESSIONID');
    res.setHeader('Access-Control-Allow-Credentials',true);
    res.setHeader('Access-Control-Expose-Headers','JSESSIONID');// 不设置可以写但浏览器无法获取
  }
  next();
})

app.get('/getData',function(req,res){
  console.log(req.headers)
  res.setHeader('JSESSIONID','ceshi');
  res.end('拜拜')
})

app.get('/getMore',function(req,res){
  res.end('second');
})

app.use(express.static(__dirname));
app.listen(4000);
```



## nginx 反向代理接口跨域

跨域原理： 同源策略是浏览器的安全策略，不是HTTP协议的一部分。服务器端调用HTTP接口只是使用HTTP协议，不会执行JS脚本，不需要同源策略，也就不存在跨越问题。





## websoket 协议跨域

浏览器与服务端的双向通信

