---
layout: page
title: 第二章 - 前置作業
permalink: /ch2/
---
***

前置作業:

如果你已經會使用D3，可以直接跳過這一章。

開始實作之前，我先簡單講解一些前置作業。要練功夫，要先把工具準備好。  
製作D3視覺化需要以下資源:  
&nbsp;&nbsp;&nbsp;&nbsp;1. 一個browser (ex: Chrome, Firefox)  
&nbsp;&nbsp;&nbsp;&nbsp;2. D3.js檔


D3程式跟一般js檔運作模式是一樣的，所以我們必須要讓我們要呈現的html檔吃到D3檔。  
D3檔取得的方法有兩種:  
&nbsp;&nbsp;&nbsp;&nbsp; 1. [下載 D3.zip](https://github.com/mbostock/d3/releases/download/v3.5.5/d3.zip)  
&nbsp;&nbsp;&nbsp;&nbsp; 2. 直接從網路上連接，也就是在html檔中加入以下這個script tag。  

{% highlight css%}
<script src="https://cdnjs.cloudflare.com/ajax/libs/d3/3.5.5/d3.min.js" charset="utf-8"></script>
{% endhighlight %}



如果以上都聽不懂沒關係，新手就直接採用方法2(網路上連接)。


```javascript
var s = 3;
   var s = "JavaScript syntax highlighting";
alert(s);
```



```python
s = "Python syntax highlighting"
print s
```



