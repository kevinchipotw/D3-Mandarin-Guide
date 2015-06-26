---
layout: page
title: 第二章 - 前置作業
permalink: /ch2/
---
***

如果你已經會使用D3，可以直接跳過這一章到第三章。

開始實作之前，我先簡單講解一些前置作業。要練功夫，要先把工具準備好。  
製作D3視覺化需要以下資源:  
&emsp; 1. 一個瀏覽器 (ex: Chrome, Firefox)  
&emsp; 2. D3.js檔
&emsp; 3. Python程式語言 (架設local伺服器用，可因個人喜好更改)
&emsp;&emsp; * 一般電腦都已經有python程式，沒有的話去<a href="https://www.python.org/downloads/" target="_blank">這裏</a>下載。


D3程式跟一般js檔運作模式是一樣的，所以我們必須要讓我們要呈現的html檔吃到D3檔。  
D3檔取得的方法有兩種:  
&emsp; 1. [下載 D3.zip](https://github.com/mbostock/d3/releases/download/v3.5.5/d3.zip), 再用一般html檔坎入js檔的方法讓html檔吃到D3檔。
&emsp; 2. 直接從網路上連接，也就是在html檔中加入以下這個script tag。  

```html
<script src="http://d3js.org/d3.v3.min.js"></script>
```


如果以上都聽不懂沒關係，新手就直接採用方法2(網路上連接)。  

跟著做就對了，先打開一個新的html檔 (檔名暫稱為: index.html)。  
打入以下的code:


```html
<!doctype html>
<html>
  <head>
    <script src ="http://d3js.org/d3.v3.min.js"></script>
  </head>
  <body>

  	<h1>我的第一個D3</h1>

  </body>
</html>
```

如果真的懶得打字(非常不建議)，或遇到問題可直接&emsp;<a href="/chapters/ch2/code/index.html" download="index"><span class = "btn btn-success">下載index.html</span></a>

在head標籤中坎入D3的js檔就能輕鬆的讓html檔跑D3的程式。看吧？夠簡單吧。
在創造完這個html檔，你一定在想說我要怎麼用我的瀏覽器執行index.html。

首先開啟terminal, cd進入index.html存放位置。

在輸入:

```python
python -m SimpleHTTPServer
```
這可以在電腦上開啟一個 local server。

範例中，index.html是放在/Users/KevinChi/Desktop/d3-mandarin-guide 裏。
Terminal輸出應如下:

```terminal
KevinChi ~ $ cd /Users/KevinChi/Desktop/d3-mandarin-guide 
KevinChi d3-mandarin-guide $ ls
index.html
KevinChi d3-mandarin-guide $ python -m SimpleHTTPServer
Serving HTTP on 0.0.0.0 port 8000 ...
```

之後再打開一個瀏覽器 (Chrome)，在URL的地方輸入:

```html
http://localhost:8000/
```


燈燈燈！瀏覽器會成功執行index.html。顯示如下:

<!-- ![browser](/chapters/ch2/img/browser.png) -->

<img src="/chapters/ch2/img/browser.png" alt="..." style= "max-height:300px" class="img-thumbnail">
<br>

實作影片:

如果不是的話，那請你先把第二章再讀一次。  
前置完成之後，接下來我們就要來累積一些實戰經驗了！Let's GO！












