关于ajax的用法

- ### 初体验案例:

  - 先创建一个index.html页面,代码如下

    ```javascript
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
    <button onclick="f1()">点我发送ajax请求</button>
    <div id="result"></div>
    <script>
        function f1() {
    
            //1.创建ajax对象
            var hu = new XMLHttpRequest();
        //4.给ajax的状态的改变设置回调函数
            hu.onreadystatechange = function () {
                if (hu.readyState == 4&&hu.status == 200) {
                    document.getElementById('result').innerText = hu.responseText;
                }
            }
            //2.建立http连接,第三个参数为true,代表异步请求
            //注意:通过localhost:3000这样的url连接的服务器,通常是http协议,而不是https
            hu.open('get','http://localhost:3000',true);
            //3.发送http连接.get请求参数为null,post请求另说
            hu.send(null)
        }
    
    
    </script>
    </body>
    </html>
    
    ```

  - 创建一个服务器 web-server.js,代码如下:

    ```javascript
    var http = require('http')
    
    var server = http.createServer()
    
    server.on('request',function (req,res) {
        //注意:一定要加上这句代码,否则报错   跟什么同源策略有关?
        
        //通常错误提示是   'Access-Control-Allow-Origin' header is present on the requested resource.   那么此时应该想到是否与下面这句代码有关.
        res.setHeader('Access-Control-Allow-Origin', "*");
        console.log('收到请求');
        res.setHeader('Content-Type', 'text/html; charset=utf-8')
        res.end('陈振虎')
    })
    
    
    server.listen(3000,function () {
        console.log('服务器已连接');
    })
    
    ```


### 关于后端怎么获取get和post请求的参数(提交的表单中的数据)

- get请求:

  ```javascript
  //首先基本的创建一个服务器代码
  
  //导入url核心模块
  var url = require('url')
  
  
  server.on('request',function (req,res) {
      //承接上面的怎么使用ajax的代码
      
      //获得get请求参数
      console.log(url.parse(req.url, true).query)  //输出的是一个对象,里面的属性值为get的请求参数
      
  }
            
            
            
       //注意:客户端发送两次请求,第一次请求是默认的,路径为 http://localhost:3000/favicon.ico,所以输出的结果又两个.第一个是一个空对象;第二个才是get的请求参数.      
            
       //增加判断 
            if(req.url !== '/favicon.ico') {}
           
  
  ```

- post请求

  ```javascript
  //首先基本的创建一个服务器代码
  
  
  //导入queryString模块
  var queryString = require('queryString')
  
  server.on('request',function (req,res) {
       //承接上面的怎么使用ajax的代码
      
      
      //获得post请求参数
      var obj = null;
          var currentData = "";
          req.on("data",function(data){
              currentData += data;
              obj = queryString.parse(currentData);
          });
          setTimeout(function () {   //注意:这里一定要异步获取(设置定时器这样的一般都是异步操作),否则会出错
              console.log(obj);    //输出的结果是post请求的参数
          },10)					
  }
  
  ```

### 案例:使用get和post请求校验用户名的唯一性

- 前端页面如下:

```javascript
//这是html页面的代码


//案例描述:用户输入用户名后,后台检验该用户名是否注册过,然后前端显示提示信息

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        #result {
            color: red;
        }
    </style>
</head>
<body>
<form action="http://localhost:3000" method="post">     //onblur失去焦点事件
    用户名:<input type="text"  id="user" name="username" onblur="f1()"> <span id="result"></span>  <br>
    密码:<input type="password" name="password">
    <button type="submit">提交</button>
</form>
<script>
    function f1() {
        //每次调用之前要将提示信息重置
        document.getElementById('result').innerText='';
        var hu = new XMLHttpRequest();
        hu.onreadystatechange=function () {
            if (hu.readyState==4 && hu.status==200) {
                //这里的responseText是后端  res.end()响应的数据
                if (hu.responseText==1){
                    //用户可用
                    document.getElementById('result').innerText='可以使用!';
                } else if (hu.responseText==0) {
                    document.getElementById('result').innerText='不能使用!';
                } else {
                    document.getElementById('result').innerText=hu.responseText;
                }

            }
        }
        //获取用户名输入框输入的信息
        var username = document.getElementById('user').value;
        console.log(username);


        //利用get请求
        // hu.open('get','http://localhost:3000/?username='+username,true);
        // console.log('111111');
        // hu.send(null);


        //利用post请求
        hu.open('post','http://localhost:3000');
        hu.setRequestHeader('Content-type','application/x-www-form-urlencoded');
        hu.send('username=' + username);


    }

</script>
</body>
</html>

```

- 后端代码

  ```javascript
  var http = require('http')
  var url = require('url')
  var queryString = require('querystring')
  var server = http.createServer()
  
  
  var array = ['虎','张三','李四','王五'];
  var user = '';
  server.on('request',function (req,res) {
      if (req.url !== '/favicon.ico'){
          res.setHeader('Access-Control-Allow-Origin', "*");
          res.setHeader('Content-Type', 'text/html; charset=utf-8')
         // user = url.parse(req.url, true).query.username;
          
          //获取post请求的参数
          var obj = null;
          var currentData = "";
          req.on("data",function(data){
              currentData += data;
              obj = queryString.parse(currentData);
          });
          
          
          //数组的forEach方法的用法
          // array.forEach(function(item,index){
          //遍历数组,传一个回调函数,item是遍历到的数据,index是这个数据的索引
      })
          
          
          
          //setTimeout(function () {
              //console.log(obj.username);
          //},10)
  
  
          	setTimeout(function(){
                   console.log(obj.username);
                   array.forEach(function (item) {
                       if (item === obj.username) {
                          return res.end(0);
                       }
                   })
               },1000);
  
     
  
  
          
      }
      
     
  })
  
  
  server.listen(3000,function () {
      console.log('服务器已连接');
  })
  
  ```

  