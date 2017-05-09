# SPA
WEB 单页面原理及实现

  
### 1.目前web端的也页面应用的实现，是通过hash值的变化实现的，我们发现，随着url地址栏#后面的字符在不停变化，页面会随之变化，且每一次变化，页面会跟随着实现局部刷新，呈现出不同的内容。 
显然，实现SPA的全部技术： 
* 一是处理#后面的字符， 
* 二是局部刷新。 
     
#### 1.1 如何处理#后的字符
 
  #后面的字符，其实是location对象的hash属性的值，即是说，我们可以轻松拿到这个#后面字符的变化值，代码如下：
```
let hash = location.hash;
```
这样我们就可以直接一个a标签跳转就能改变hash值。
```
  <a href="#index">首页</a>;
  <a href="#news">新闻</a>;
  <a href="#mine">我的</a>;
```
第一个问题就这样解决了。
#### 1.2 如何实现局部刷新

利用ajax的技术可以顺利实现
### 2.贴代码
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        a{
            text-decoration: none;
            color: #000;
            border: 1px solid maroon;
        }
        div{
            width: 300px;
            height: 300px;
            background-color: gray;
            margin-top: 10px;
            font-size: 20px;
        }
    </style>
</head>
<body>
  <a href="#index">首页</a>
  <a href="#news">新闻</a>
  <a href="#mine">我的</a>
<div id="conment"></div>


<script src="http://cdn.bootcss.com/jquery/1.8.3/jquery.js"></script>
<script>
    //通过hashchange事件来监听hash值的变化，直接使用onhashchange也是一样
    window.addEventListener('hashchange',function(){
        //拿到#后面的字符，即是URL的锚部分
        var hash = document.location.hash;
        //去掉query部分
        hash=hash.split("?")[0]
        //通过判断不同的hash值，从而请求不同的数据来渲染页面
        // 对switch不熟悉，使用if elseif  else 也是一样
        switch (hash){
            case '#index':
                    //这里是我封装的AJAX
                $.ajax({
                    url:'./json/index.json',
                    success:function(result){
                        
                       document.getElementById('conment').innerText =JSON.parse(result)[0].name;
                    }
                });
            break;
            case '#news':
                $.ajax({
                    url:'./json/news.json',
                    success:function(result){
                        document.getElementById('conment').innerText =JSON.parse(result)[0].name;
                    }
                });
            break;
            case '#mine':
                $.ajax({
                    url:'./json/mine.json',
                    success:function(result){
                        document.getElementById('conment').innerText =JSON.parse(result)[0].name;
                    }
                });
            break;
            default :
                $.ajax({
                    url:'./json/index.json',
                    success:function(result){
                        document.getElementById('conment').innerText =JSON.parse(result)[0].name;
                    }
                });
        }
    });
</script>
</body>
</html>
```
.json文件的结构
```
[{"namwe":"index"}]

```
### 单页面就这样能够实现了
