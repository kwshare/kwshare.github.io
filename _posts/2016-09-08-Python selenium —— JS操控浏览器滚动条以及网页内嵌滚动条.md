---
layout: post
title:  "Python selenium —— JS操控浏览器滚动条以及网页内嵌滚动条"
date:   2016-09-08 09:40:15
categories: selenium
permalink: /archivers/browser-scroll-bar
---

今天博主给大家分享一下用JS控制浏览器滚动条的办法。

## **1.兼容Firefox、Chrome、IE的浏览器滚动JS**

经常有人会发现自己写的JS能够控制某个浏览器滚动条，但是却在另一个浏览器上不灵了，博主今天带给大家集中能够兼容Firefox、Chrome以及IE的滚动条滚动方法：


```JavaScript
$(window).scrollTop(300);
$(document).scrollTop(300)
$("html,body").scrollTop(300);
```

都是jQuery的写法，原生js怎么办：

```JavaScript
document.body.scrollTop = 300; // FireFox  IE9+ 不可以
document.documentElement.scrollTop = 300; // Chrome 不可以 document.documentElement  === html
```

没办法，以上两种写法，都是一个可以一个不行。所以还是用上面的jQuery的写法吧，要么你就自己判断浏览器类型从而选取不同的原生js写法。。

参考：**[传送门](http://liyaoli.com/2015-08-17/about-scroll.html)**

## **2.如何控制浏览器内嵌div的滚动条**


很多人疑惑怎么用selenium控制网页div中滚动条的滚动，其实这个问题很简单，用JS很简单就可以实现。
示例HTML代码如下：

```html
<!DOCTYPE html>
<html>
<head>
<style type="text/css">
div.scroll
{
background-color:#00FFFF;
width:100px;
height:100px;
overflow:auto;
}

</style>
</head>

<body>

<p>overflow:scroll</p>
<div class="scroll">You can use the overflow property when you want to have better control of the layout. The default value is visible.aaaaaaaaaaaaaaaaaaaaaaaaaaaa</div>

</body>
</html>
```

接下来我们用JS来控制里面的滚动条滚动：

```python
from selenium import webdriver
dr=webdriver.Firefox()
dr.get('file:///D:/1.html')
js='document.getElementsByClassName("scroll")[0].scrollTop=10000' 
# 就是这么简单，修改这个元素的scrollTop就可以
dr.execute_script(js)
```

当然，我们能做更多：

```JavaScript
document.getElementsByClassName("scroll")[0].scrollHeight // 获取滚动条高度
document.getElementsByClassName("scroll")[0].scrollWidth // 获取横向滚动条宽度
document.getElementsByClassName("scroll")[0].scrollLeft=xxx // 控制横向滚动条位置
```

总结一下：

要想滚动内嵌div的滚动条，我们可以用js获取到该元素，然后使用以下方法：

```JavaScript
元素.scrollTop=xxx  // 纵向滚动到xxx位置，0是最顶端
元素.scrollLeft=xxx  // 横向滚动到xxx位置，0是最左端
```




