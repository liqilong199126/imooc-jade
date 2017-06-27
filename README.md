# imooc-jade
学习Jade模板引擎

# jade模板引擎学习笔记（WebsStorm9.0.3+ nodejs+express+jade） #
- jade环境搭建 
- jade标签写法 
- jade注释
- jade添加类名、id、属性  
- jade添加脚本，css
- jade变量
- jade多行文本显示
- jade流程代码:for,each,while
- jade流程代码：if - else - unless ，case
- 可重用的jade块Mixins
- 模板继承（extends）
- 模板包含（include）

## jade环境搭建 ##
 
打开WebsStorm9.0.3，File—New Project…，project type选择Node.js Express App，新建项目jadeTest，打开Terminal，输入npm install 安装程序需要的依赖项，安装成功后，环境就搭好了，打开app.js文件，找到jade模板引擎的引用代码如下

    1 var express = require('express');
    2 var app = express();
    3 app.set('views', path.join(__dirname, 'views'));
    4 app.set('view engine', 'jade');
 



接下来，我们开始学习jade语法，程序的默认页面是index.jade,打开index.jade,然后在Terminal中输入以下命令：

    jade -P -w index.jade

**命令行：jade -P -w index.jade 实时监控jade文件，自动编译为不压缩的html文件，方便实时查看写的jade代码和html的比较**

 ## jade标签写法

index.jade


```
1 doctype html
2 html
3     head
4         title jade标签写法
5     body
6         P 文档声明：doctype html
7         P 标签省去尖括号，元素和文本用空格间隔
8         div
9             P 元素的父子关系用空格缩进表示
```

编译成html：

 
```
1 <!DOCTYPE html>
 2 <html>
 3   <head>
 4     <title>jade学习</title>
 5   </head>
 6   <body>
 7     <P>文档声明：doctype html</P>
 8     <P>标签省去尖括号，元素和文本用空格间隔</P>
 9     <div>
10       <P>元素的父子关系用空格缩进表示</P>
11     </div>
12   </body>
13 </html>
```



## jade注释　

  **单行注释： //**

  编译成html：<!-- 单行注释 --> 


```
1 doctype html
2 html
3     head
4         title jade学习
5     body
6          p 单行注释://
7         //div
8              p 测试单行注释
```

编译成html

 
```
1 <!DOCTYPE html>
 2 <html>
 3   <head>
 4     <title>jade学习</title>
 5   </head>
 6   <body>   
 7     <p>单行注释://</p>
 8     <!--divp 测试单行注释
 9     -->
10      </body>
11 </html>
```


 **块注释：//**


```
1 doctype html
2 html
3     head
4         title jade学习
5     body       
6         p 块注释：//
7         //
8             div
9                p 测试块注释
```

编译成html


```
1 <!DOCTYPE html>
 2 <html>
 3   <head>
 4     <title>jade学习</title>
 5   </head>
 6   <body> 7    
 7     <p>块注释：//</p>
 8     <!--
 9     div
10        p 测试块注释
11     -->
12   </body>
13 </html>
```



**非缓存注释：注释的内容不会显示在编译的html中**




```
1 doctype html
2 html
3     head
4         title jade学习
5     body
6         P 非缓存注释/块注释：//-
7         //-div
8             p 测试多行注释
9
```

编译成html


```
1 <!DOCTYPE html>
2 <html>
3   <head>
4     <title>jade学习</title>
5   </head>
6   <body>    
7     <P>非缓存注释/块注释：//-</P>
8   </body>
9 </html>
```

 

## jade添加类名、id、属性  

 




```
1 doctype html
2 html
3     head
4         title jade学习
5     body
6        div.className#idName
7            p.className
 类名加点紧跟元素后面或者id后面，不用加空格，后面紧跟的文本属性要加空格
8            p#idTest id名加#紧跟元素后面或者类后面，不用加空格，后面紧跟的文本要加空格
9        #testDiv div如果有className/id，可以省略元素div
10        .classDiv div如果有className/id，可以省略元素div
11        h1 属性添加
12        .className
13            p 属性放在小括号里，紧跟元素/id/ClassName后面，属性之间用逗号隔开,id或class也可以放在括号内
14            input.classP(id='content',type='text',value="添加属性")
```

编译成html

 
```
1 <!DOCTYPE html>
2 <html>
3   <head>
4     <title>jade学习</title>
5   </head>
6   <body>
7     <div id="idName" class="className">
8       <p class="className">类名加点紧跟元素后面或者id后面，不用加空格，后面紧跟的文本属性要加空格</p>
9       <p id="idTest">id名加#紧跟元素后面或者类后面，不用加空格，后面紧跟的文本要加空格</p>
10     </div>
11     <div id="testDiv">div如果有className/id，可以省略元素div</div>
12     <div class="classDiv">div如果有className/id，可以省略元素div</div>
13     <h1>属性添加</h1>
14     <div class="className">
15       <p>属性放在小括号里，紧跟元素/id/ClassName后面，属性之间用逗号隔开,id或class也可以放在括号内</p>
16       <input id="content" type="text" value="添加属性" class="classP">
17     </div>
18   </body>
19 </html>
```

 

## Jade添加脚本，css 

 
```
1 doctype html
2 html
3     head
4         meta
5         title #{title}
6         style.
7             .className{
8                 background: red;
9                 width:200px;
10             }
11             #id1{
12                 background: blue;
13                 width: 200px;
14             }
15         script.
16             var s='test';
17     body
```

编译成html

 
```
1 <!DOCTYPE html>
2 <html>
3   <head>
4     <meta>
5     <title></title>
6     <style>
7       .className{
8           background: red;
9           width:200px;
10       }
11       #id1{
12           background: blue;
13           width: 200px;
14       }
15     </style>
16     <script>var s='test';</script>
17   </head>
18   <body>
19   </body>
20 </html>
```

 

## jade变量

 服务器端代码：以 ```'-'```开头的代码

 变量的引用方式：

   
```
#{表达式}    
= 表达式
!{表达式}
!= 表达式
```



```
1 doctype html
2 html
3     head
4         title jade学习
5     body
6         -var test="以'-'开头写服务器端代码"
7         p #{test}
8         -var str='test1' ;
9         -var strTest='<div><p>变量调用</p></div>';
10         p #{str.toUpperCase()}
11         p= str
12         //转义引用，(#{表达式} 等价于 =表达式)
13         p #{strTest}
14         p= strTest
15         //非转义引用，(!{表达式}等价于 !=表达式)
16         p !{strTest}
17         p!= strTest
```

 编译成html

 
```
1 <!DOCTYPE html>
2 <html>
3   <head>
4     <title>jade学习</title>
5   </head>
6   <body>
7     <p>以'-'开头写服务器端代码</p>
8     <p>TEST1</p>
9     <p>test1</p>
10    <!--转义引用，(#{表达式} 等价于 =表达式)-->
11    <p>&lt;div&gt;&lt;p&gt;变量调用&lt;/p&gt;&lt;/div&gt;</p>
12    <p>&lt;div&gt;&lt;p&gt;变量调用&lt;/p&gt;&lt;/div&gt;</p>
13    <!--非转义引用，(!{表达式}等价于 !=表达式)-->
14    <p><div><p>变量调用</p></div></p>
15    <p><div><p>变量调用</p></div></p>
16   </body>
17 </html>
```

直接显示```#{title}```表达式引用方法：

```
p \#{title}
p \!{title}
```


编译成html

```
<p>#{title}</p>
<p>!{title}</p>
```

注意：


```input(value=data)```,```data```有值就显示值，没有值就什么也不显示
```input(value=#{data})data```有值就显示值，没有值显示```undifined```
模板里的数据优先级高于外部传进来的数据

可以传递json数据

可以对表达式进行进行操作，例如：

 ```1 -var c='test1' ; 2 p #{c.toUpperCase()} ```
 
编译成html为：

```<p>TEST1</p>```
## jade多行文本显示 

### 多行文本显示有2中方式

#### 1.标签后边紧跟点 



```
p#id2.className.
       22222
       <strong>6666</strong>
       3333
       <span>888</span>
       4444
       555
```

####  2.标签后面的文本以|开头 

 
```
p#id3
 |222
 strong 888
 |3333
 span 9999
 |444
```


  

## jade流程代码:for,each,while

### for
#### 遍历数组的for
     
```
-var arry=[1,3,5,7,9];
ul
    -for (var i=0;i<arry.length;i++)
    li= arry[i]
```

     
编译成html

 
```
<ul>
    <li>1</li>
    <li>3</li>
    <li>5</li>
    <li>7</li>
    <li>9</li>
</ul>
```


#### 遍历对象属性的for
      
```
-var json={name:'tom',age:9,phone:13222222222};
-for(var j in json)
 p= json[j]
```

编译成html


```
<p>tom</p>
<p>9</p>
<p>13222222222</p>
```


### each
#### 遍历数组
    
```
-var arry=[1,3,5,7,9];
-each value,index in arry
  p #{index}:#{value}
each item in arry
  p= item
```

  编译成html

    
```
<p>0:1</p>
<p>1:3</p>
<p>2:5</p>
<p>3:7</p>
<p>4:9</p>
<p>1</p>
<p>3</p>
<p>5</p>
<p>7</p>
<p>9</p>
```

#### 遍历json数据
     
```
-var json={name:'tom',age:9,phone:13222222222};
ul
 -each value,key in json
  li #{key}:#{value}
```

编译成html
   
```
<ul>
    <li>name:tom</li>
    <li>age:9</li>
    <li>phone:13222222222</li>
</ul>
```


###while 


```
-var j=0;
    ul
        while j<3
           li= j++
```

　　编译成html



```
<ul>
    <li>0</li>
    <li>1</li>
    <li>2</li><br> 
</ul>
```

## 　jade流程代码：if - else - unless ，case

###    if - else - unless 　


```
-var arry=['hello','world','good','test']
 if arry
    if(arry.length>2)
      div
           p= arry[0] +':if'
           p= arry[1]+':if'
    else
      p 数组长度等于小于2
 else
   p 数组为空
 unless arry.length<=2
   div
       p= arry[0]
       p= arry[1]
```

编译成html

```
<div>
    <p>hello:if</p>
    <p>world:if</p>
</div>
<div>
    <p>hello</p>
    <p>world</p>
</div>
```

注: unless 相当于非，unless false 才执行代码

###  case

case相当于switch

 


```
-var arry=['hello','world','good','test']
  each item in arry
         case item
            when 'hello'
            when 'world'
              p hello Tom!
            when 'good': P Good News
            default
               P #{item}
```

 

　　编译成html

    
```
<p>hello Tom!</p>
<p>hello Tom!</p>
<P>Good News</P>
<P>test</P>
```

---

<span style="font-size: 16px; background-color: #ffff00;">
注意：</span><br>when 'world'
   p hello Tom!<br>或者when 'good': P Good News <br>效果是一样的



## 可重用的jade块Mixins

###  1.Mixins简单说就是代码块复用

      //定义代码块
      mixin bags
        div.allBags
           p 书包
           p 文具包
           p 公文包
           p 工具包
      //调用
      +bags
编译成html


```
<!--定义代码块-->
<!--调用-->
    <div class="allBags">
      <p>书包</p>
      <p>文具包</p>
      <p>公文包</p>
      <p>工具包</p>
    </div>
```

###   2.可以为mixin定义参数 　　


```
//参数个数确定
mixin parameters(name,age)
  p #{name}今年#{age}岁
+parameters('小明',6)
+parameters('小强',8)


 
//参数个数不确定
mixin parameterList(name,...items)
  h1= name
  ul
    each nn in items
     li= nn
+parameterList('小明','早晨读书','中午练书法','下午练拳')
``` 

　　编译成html


```
<!--参数个数确定-->
        <p>小明今年6岁</p>
        <p>小强今年8岁</p>
    <!--参数个数不确定-->
        <h1>小明</h1>
        <ul>
          <li>早晨读书</li>
          <li>中午练书法</li>
          <li>下午练拳</li>
        </ul>
```

### 　3.mixin可以嵌套使用　

    
```
mixin bags
    div.allBags
        p 书包
        p 文具包
        p 公文包
        p 工具包
      //调用
     
      mixin getBags(name)
        P(class= name) 请列举包的种类
        +bags
      +getBags('back')
```

编译成html

           
```
<P class="back">请列举包的种类</P>
<div class="allBags">
    <p>书包</p>
    <p>文具包</p>
    <p>公文包</p>
    <p>工具包</p>
</div>
```

### 4.mixin可以从外部传入代码块


```
mixin bags
        div.allBags
           p 书包
           p 文具包
           p 公文包
           p 工具包
           //block:外部传入的代码块关键字
           if block
              block

 +bags
        h1 外部代码块
        div
            p 外部代码块1
            p 外部代码块2
```

编译成html


```
<div class="allBags">
          <p>书包</p>
          <p>文具包</p>
          <p>公文包</p>
          <p>工具包</p>
          <!--block:外部传入的代码块关键字-->
          <h1>外部代码块</h1>
          <div>
            <p>外部代码块1</p>
            <p>外部代码块2</p>
          </div>
 </div>
```

### 5.mixin支持传递属性

     mixin GetAttrs(name1,name2)
         h1 传递属性的方法1
         p(class!=attributes.class)= name1
         h1 传递属性的方法2
         p&attributes(attributes)= name2

      +GetAttrs('方法1','方法2')(class='redColor',id='passId')
编译成html

        
```
<h1>传递属性的方法1</h1>
<p class="redColor">方法1</p>
<h1>传递属性的方法2</h1>
<p id="passId" class="redColor">方法2</p>
```

##  模板继承（extends）

继承者里如果与模板里有同名的block，继承者里同名的block会覆盖掉模板里的block

layout.jade


```
doctype html
html
  head
    title= title
    link(rel='stylesheet', href='/stylesheets/style.css')
  body
```

index7.jade


```
//layout.jdae与index7.jade是同一个目录下
extends layout
block content
    p 继承模板layout
```

index7.jade编译成html



```
<!DOCTYPE html>
<html>
  <head>
    <title></title>
    <link rel="stylesheet" href="/stylesheets/style.css">
  </head>
  <body>
    <p>继承模板layout</p>
  </body>
</html>
```

　

## 模板包含（include）

**把很多块引用到一个页面中**

index8.jade


```
doctype html
html
    head
       include ../templates/head
    body
        p 引入静态的jade css
        include ../templates/css
        p 引入html文件
        include  ../templates/content.html
        P 引入页脚模块
        include ../templates/footer
```

编译成html


```
<!DOCTYPE html>
<html>
  <head>
    <title></title>
    <link rel="stylesheet" href="/stylesheets/style.css">
  </head>
  <body>
    <p>引入静态的jade css</p>
    <style>
      p{
      background:blue;
      }
    </style>
    <p>引入html文件</p><div>引用html</div>
    <P>引入页脚模块</P>
    <div>页脚模块</div>
  </body>
</html>
```

　　

下面这些文件的位置是在index8.jade上一级目录templates中

head.jade


```
title= title
link(rel='stylesheet', href='/stylesheets/style.css')
```

css.jade


```
style.
    p{
    background:blue;
    }
```

content.html


```
<div>引用html</div>
```

footer.jade


```
div 页脚模块
```
