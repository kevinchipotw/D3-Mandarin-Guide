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
&emsp; 1. 一個browser (ex: Chrome, Firefox)  
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
跟著做就對了，先打開一個新的html檔。打入以下的code:


```html
<!doctype html>
<html>
  <head>
    <script src ="http://d3js.org/d3.v3.min.js"></script>
  </head>

  <body>

  </body>
</html>
```

在head標籤中坎入D3的js檔就能輕鬆的讓html檔跑D3的程式。看吧？夠簡單吧。
前置完成之後，接下來我們就要來累積一些實戰經驗了！Let's GO！












