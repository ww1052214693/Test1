# 响应是开发(bootstrap框架)

### 插件 库 框架的概念

- 插件:提供单一的功能
- 库:包含多种功能(函数)
- 框架:分为 ui框架和js框架;前者是专注界面的,后者是开发思想(mvc或mvvm)

### 响应式开发概念

- 为什么使用响应式开发:  开发一个页面能够适应多个终端(pc端  移动端  pad),节约成本
- 使用场景:新开发的页面可以使用响应式开发; 旧页面改为响应式比较耗费成本

### 响应式的原理

- css3 媒体查询:通过查询 Screen 的宽度来指定某个宽度区间的网页布局
- 超小屏幕(手机) :   768px以下   
- 小屏幕(pad):    768px ~ 992px
- 中屏幕(大屁股电脑):  992px ~ 1200px
- 宽屏设备(笔记本): 1200px以上

### 响应式实现

- 一般的页面都会设置版心

  ```javascript
  .container {
      width:100%
      background-color:red
      height:1000px(方便观察效果,一般由内容撑开)
      margin: 0 auto
  }
  ```

- ```
  1. 在超小屏设备的时候 768px以下      当前容器的宽度100%     背景蓝色
  ```

- ```
  2. 在小屏设备的时候   768px-992px    当前容器的宽度750px    背景绿色
  ```

- ```
  3. 在中屏设备的时候   992px-1200px   当前容器的宽度970px    背景红色
  ```

- ```
  4. 在大屏设备的时候   1200px以上      当前容器的宽度1170px   背景黄色
  ```

- ##### 媒体查询的格式

  ```javascript
  <style>
      
      @media screen and(max-width: 768px){}  ---->超小屏幕
      
      
      @media screen and(min-width: 768px) and (max-width:992px) {}   小屏幕
      
      等等
  
  
  	
      
      
      </style>
  ```

### bootstrap框架

- 为什么使用:
  - 开发效率更高
  - 提供了一系列简洁 直观 强悍的组件
  - 标准化的 html + css 编码规范
  - 有自己的生态圈,不断更新迭代
  - 虽然样式界面已经定义好,但是用户可以自定义,修改默认的样式
- 3.xx版本使用率最高:稳定,但是放弃了对 ie6 7 ,对ie8支持,但界面效果不好(css3的属性),偏向于响应式布局 移动端优先的web项目



### bootstrap框架的基本模板

```javascript
<!--h5文档申明-->
<!DOCTYPE html>
<!--文档语言申明  en zh-CN zh-tw -->
<html lang="zh-CN">
<head>
    <!--文档编码申明-->
    <meta charset="utf-8">
    <!--要求当前网页使用浏览器最高版本的内核来渲染-->
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <!--视口的设置：视口的宽度和设备一致，默认的缩放比例和PC端一致，用户不能自行缩放-->
    <meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=0">
    <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
    <!-- 优先加载和浏览器解释 -->

    <title>title</title>

    <!-- Bootstrap 核心样式-->
    <link href="../lib/bootstrap/css/bootstrap.css" rel="stylesheet">
    <!-- html5shiv 和  respond 分别用来解决IE8版本浏览器不支持 H5标签和媒体查询的  不兼容问题-->
    <!-- HTML5 shiv and Respond.js for IE8 support of HTML5 elements and media queries -->
    <!-- 警告：不能以file形式打开，本地打开。最好http://打开 -->
    <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
    <!-- 在 IE 9 一下引入-->
    <!--[if lt IE 9]>
    <script src="../lib/html5shiv/html5shiv.min.js"></script>
    <script src="../lib/respond/respond.min.js"></script>
    <![endif]-->
</head>
<body>
<!--TODO-->
<!-- Button trigger modal -->
<button type="button" class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal">
    Launch demo modal
</button>

<!-- Modal -->
<div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel">
    <div class="modal-dialog" role="document">
        <div class="modal-content">
            <div class="modal-header">
                <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
                <h4 class="modal-title" id="myModalLabel">Modal title</h4>
            </div>
            <div class="modal-body">
                ...
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
                <button type="button" class="btn btn-primary">Save changes</button>
            </div>
        </div>
    </div>
</div>



<!-- bootstrap依赖jquery-->
<!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
<script src="../lib/jquery/jquery.min.js"></script>
<!-- bootstrap js 核心文件-->
<!-- Include all compiled plugins (below), or include individual files as needed -->
<script src="../lib/bootstrap/js/bootstrap.min.js"></script>
</body>
</html>
```

### 关于 Nomalize.css

- 用来重置样式库,和开发人员自定义的 reset.css 一样,用来增强浏览器的表现一致性
- 注意:nomalize 不会重置已经一致的元素,如 ul 中 li 前面的圆点,所有浏览器中li前面都有一个圆点

### bootstrap常用的类名

- ```javascript
  .container       设置响应式版心(bootstrap内部以实现媒体查询功能), 
      
      //.container容器默认有15px的左右内间距,
      //.row 填充父容器的15px的左右内间距   margin-left,margin-right -15px拉伸
  ```

- ```javascript
  .container-fluid      流式布局(宽度100%)
  ```



- ``` javascript
  //栅格系统中常用的类名
  
  .row      //设置一行
  .col-*-*    //设置一列
  .col-xs-offset-1      //设置列的偏移,因为列是左对齐,所以偏移是向右偏
  .col-xs-push-9        //向后推9份
  .col-xs-pull-9        //向前拉 9份
  ```

- ```javascript
  //响应式 控制元素的隐藏/显示
  .hidden-lg   .hidden-md   .hidden-sm   .hidden-xs
  ```

- 折叠组件(详情见bootstrap官网)

  ```javascript
  //主要作用就是隐藏和显示元素
  <button data-toggle='collapse' data-target='.d1' >切换</button>    
  // data-toggle='collapse'   申明是什么组件(这里的collapse是折叠组件)
  // data-target = '(这里要写一个选择器,如: .d1)',将哪个元素折叠起来
  <div class='d1'>
  .....    
  ....    
   ....   
      
  </div>
  ```

-  ```javascript
   // .aria-*      只要类名带这个 aria的  可要可不要,删掉没影响
   // .sr-only     也是一样的
   ```

-  

### 格系统的基本使用

  ```javascript
<!--h5文档申明-->
<!DOCTYPE html>
<!--文档语言申明  en zh-CN zh-tw -->
<html lang="zh-CN">
<head>
    <!--文档编码申明-->
    <meta charset="utf-8">
    <!--要求当前网页使用浏览器最高版本的内核来渲染-->
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <!--视口的设置：视口的宽度和设备一致，默认的缩放比例和PC端一致，用户不能自行缩放-->
    <meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=0">
    <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
    <!-- 优先加载和浏览器解释 -->

    <title>title</title>

    <!-- Bootstrap 核心样式-->
    <link href="../lib/bootstrap/css/bootstrap.css" rel="stylesheet">
    <!-- html5shiv 和  respond 分别用来解决IE8版本浏览器不支持 H5标签和媒体查询的  不兼容问题-->
    <!-- HTML5 shiv and Respond.js for IE8 support of HTML5 elements and media queries -->
    <!-- 警告：不能以file形式打开，本地打开。最好http://打开 -->
    <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
    <!-- 在 IE 9 一下引入-->
    <!--[if lt IE 9]>
    <script src="../lib/html5shiv/html5shiv.min.js"></script>
    <script src="../lib/respond/respond.min.js"></script>
    <![endif]-->
    <style>
        .container{
            height: 100px;
            background: pink;
        }
        .container > .row{
            height: 50px;
            background: green;
        }
        .container > .row > div{
            height: 25px;
            border: 1px solid #ccc;
        }
    </style>
</head>
<body>
<!--响应式布局容器-->
<div class="container">
    <!--栅格系统：其实就是行和列的布局，网格状布局-->
    <!--行：row-->
    <!-- .container容器默认有15px的左右内间距  .row 填充父容器的15px的左右内间距   margin-left,margin-right -15px拉伸 -->
	//row 代表一行,默认一行为12等分
    <div class="row">
        <!--列：col-*-*  *不确定（参数） -->
        <!--
            col：列样式
            第一个*：屏幕的大小
            大屏设备     lg   大屏设备以上生效包含本身
            中屏设备     md   中屏设备以上生效包含本身
            小屏设备     sm   小屏设备以上生效包含本身
            超小屏设备   xs   超小屏设备以上生效包含本身
            第二个*：每一行的分等份，默认分成12等份 ，数字代表的是占多少份
        -->
		// col代表一列
        <div class="col-xs-4"></div>
        <div class="col-xs-4"></div>
        <div class="col-xs-4"></div>
    </div>
</div>
<!-- bootstrap依赖jquery-->
<!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
<script src="../lib/jquery/jquery.min.js"></script>
<!-- bootstrap js 核心文件-->
<!-- Include all compiled plugins (below), or include individual files as needed -->
<script src="../lib/bootstrap/js/bootstrap.min.js"></script>
</body>
</html>
  ```

#### 栅格系统案例

```javascript
 <style>
        .container{
            height: 100px;
            background: pink;
        }
        .container > .row{
            height: 50px;
            background: green;
        }
        .container > .row > div{
            height: 25px;
            border: 1px solid #ccc;
        }
 </style>






<body>
<!--
大屏设备   让div平均分成6等份
中屏设备   让div平均分成4等份
小屏设备   让div平均分成3等份
超小屏设备 让div平均分成2等份
-->
<div class="container">
    <div class="row">
        <div class="col-lg-2 col-md-3 col-sm-4 col-xs-6"></div>
        <div class="col-lg-2 col-md-3 col-sm-4 col-xs-6"></div>
        <div class="col-lg-2 col-md-3 col-sm-4 col-xs-6"></div>
        <div class="col-lg-2 col-md-3 col-sm-4 col-xs-6"></div>
        <div class="col-lg-2 col-md-3 col-sm-4 col-xs-6"></div>
        <div class="col-lg-2 col-md-3 col-sm-4 col-xs-6"></div>
    </div>
</div>



<!-- bootstrap依赖jquery-->
<!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
<script src="../lib/jquery/jquery.min.js"></script>
<!-- bootstrap js 核心文件-->
<!-- Include all compiled plugins (below), or include individual files as needed -->
<script src="../lib/bootstrap/js/bootstrap.min.js"></script>
</body>

```

#### 栅格系统的扩展

```javascript
<div class="container">
    <div class="row">
        <!--栅格嵌套-->
        <div class="col-xs-4">
            <div class="row">
                <div class="col-xs-6"></div>
                <div class="col-xs-6"></div>
            </div>
        </div>
        <!--列的偏移-->(比如说一行中,第一列占3份,第二列占6份,中间空出3份的空间,实现这样的效果,需要用到列的偏移)
        <div class="col-xs-4">
            <div class="row">
                <div class="col-xs-3"></div>
                <div class="col-xs-6 col-xs-offset-1"></div>
            </div>
        </div>
        <!--列的排序-->(第一列占3份,第二列占9份,正常情况下,3份在前,9份在后;要实现9份在前,3份在后,此时就要用到列的排序)
        <div class="col-xs-4">
            <div class="row">
                <!--
                push 往后推
                pull 往前拉
                -->
                <div class="col-xs-3 col-xs-push-9">col-xs-3</div>
                <div class="col-xs-9 col-xs-pull-3">col-xs-9</div>
            </div>
        </div>
    </div>
</div>
```

### 关于怎么覆盖Bootstrap的默认样式

- 首先例如 .navbar-default  是导航栏的默认样式类,我们需要根据要求定义自己的样式
- 然后  Ctrl + 鼠标左键  查看源码,将这个包含默认样式的选择器的所有源代码粘贴到自己的css文件中,将源码中的  .navbar-default 这个选择器名全部换成自定义的名字 (Ctrl+r)
- 最后 借助浏览器的开发者工具 定位到需要修改样式的位置进行修改样式