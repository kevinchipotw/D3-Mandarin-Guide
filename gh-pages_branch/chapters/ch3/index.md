---
layout: page
title: 第三章 - 長條圖
permalink: /ch3/
---
***

#### 成品圖:  

<img src="/chapters/ch3/img/product.png" alt="..." style= "max-height:300px" class="img-thumbnail">

<a href="/chapters/ch3/code/index.html" download="index"><span class = "btn btn-success">下載長條圖成品</span></a>

***

#### 製作步驟: 
首先照第二章的前置作業先將開一個local server執行index.html (不會的話請先詳閱第二章)
index.html的code應如下:

```html
<!doctype html>
<html>
  <meta charset="UTF-8">
  <head>
    <script src ="http://d3js.org/d3.v3.min.js"></script>
  </head>
  <body>
  	<h1>我的第一個D3</h1>

  </body>
</html>
```

之後再body標籤中輸入script標籤，讓html檔知道你輸入的code為js code。
像這樣:

```html
<body>
  <h1>我的第一個D3</h1>
  <script type="text/javascript">

  </script>

</body>
```

現在我們就要開始做D3的編程了！
**以下的程式碼務必打在上面的script tag裡。**
像這樣:

```html
<script type="text/javascript">
	// 以下的code...
</script>
```
懂了嗎? 這個指示很重要。

首先我們要先設定svg的性質，因為我們要在svg上呈現我們的資料圖形。
可以將svg想成一塊布，當你要畫在一塊布上面的時候，是否先決定布的大小? D3同理。
所以接下來我們所輸入的code你將不會在瀏覽器上看到圖形，因為我們要先訂出我們的白布的尺寸。
(因為是白色的所以看不到...)
GO!

先宣布兩個數值: 

```javascript
var svg_width = 500;
var svg_height= 200;
```
svg_width = svg寬度
svg_heigh = svg長度
這兩個值是我們之後要用來設定svg(布)的長寬用的。
**但目前只是訂出了大小，但還設定svg！**
之後加上:

```javascript
var dataset = [ 30, 20, 10, 40, 45 , 25, 15, 35 , 18];
```
這是我們要視覺化的data。
這邊先稍微講解一下這個data的結構，dataset的結構為array。
因此我們如果要取得裡面的一個值，可以用 _dataset[i]_。
i 為元素指數(數字)。
EX: 如果我要取得dataset中 '10' 這個值。
可以用 _dataset[2]_。
這個如果不懂的話，先去看看一些Javascript data結構的書再繼續讀。
這邊不做過多解釋。

在輸入完dataset之後，我們要用我們之前訂出的大小來**設定svg了**。
輸入:

```javascript
var svg = d3.select("body")
	.append("svg")
	.attr("width", svg_width)
	.attr("height", svg_height);
```
看不懂嗎? 沒關係，這就是為什麼你要看這本實戰手冊。
首先，可以先看等號的右邊的編程。

```javascript
d3.select("body")
```
這行code是我們在跟D3說我要把元素加在body標籤中。
記得這個嗎?

```html
<!doctype html>
<html>
  <meta charset="UTF-8">
  <head>
    <script src ="http://d3js.org/d3.v3.min.js"></script>
  </head>
  <body>
  	<h1>我的第一個D3</h1>

  </body>
</html>
```
我們在跟D3說我們要把元素加在<body>跟</body>之間。
我們要加什麼東西呢？

```javascript
d3.select("body")
  .append("svg")
```
加svg，append的中文就是加上的意思。
所以append("svg")就是說我要在body標籤中加上svg元素。
Easy~
接下來:

```javascript
d3.select("body")
  .append("svg")
  .attr("width", svg_width)
  .attr("height", svg_height);
```
這兩行attr程式碼，就是我們在跟D3說svg的大小。
前面我們不是有設定svg_width 跟 svg_height？

```javascript
var svg_width = 500;
var svg_height= 200;
```
現在這兩行attr就是在用那兩個數值來設定svg的長寬。

現在我們的code有:

```html
<script type="text/javascript">
  var svg_width = 500;
  var svg_height = 200;

  var dataset = [ 30, 20, 10, 40, 45 , 25, 15, 35 , 18];

  var svg = d3.select("body")
        .append("svg")
        .attr("width", svg_width)
        .attr("height", svg_height);

</script>
```
現在我們已經在我們的html文件中有一個寬500px * 長200px的svg元素和我們要呈現的data array。

OK，先深呼吸。因為接下為重頭戲。
現在我們必須把data呈現/畫到我們所設定的svg上。
怎麼做呢？
輸入: 

```javascript
svg.selectAll("rect")
         .data(dataset)
         .enter()
         .append("rect")
```
許多人都認為這是D3最難懂的地方，不過其實理解後道理其實很簡單。

```javascript
svg.selectAll("rect")
```
這行code先select(選擇)了我們html文件中的 "rect" 元素。
也許你會說我們在文件上並沒有任何 "rect" 元素，那D3要如和選擇那些元素呢？
其實D3在這個地方所做的是一個empty selection。也就是說他沒有選擇任何元素。
D3選擇的是你未來要加入到html文件中的元素。
先繼續看下去。

```javascript
.data(dataset)
```
這行是說，我們要用的data是我們已經宣告的dataset array

```javascript
.enter()
```
_.enter()_ 是一個比較特殊的語法。
可以把它想成一個過濾網，過濾掉data值。
那他是要過濾掉什麼data值呢？
_.enter()_ 會過濾掉html上已經有 "rect" (我們的empty selection) 元素代表的data值。
因為dataset中的data值都沒有 "rect" 這個元素代表。所以所有在dataset中的data值都不會被排除/過濾。
而通過.enter所過濾的所有值都會執行.enter()以下的指令。
所以以我們的dataset來講:

```javascript
var dataset = [ 30, 20, 10, 40, 45 , 25, 15, 35 , 18];
```
因為所有的值(30, 20, 10, ...)，總共9個data值都沒有被過濾掉。
所以 _.enter()_ 以下的指令都會被執行9次，每次使用一個dataset裡面的一個值。

<br>

```javascript
.append("rect")
```
這句比較好懂，簡單的說，就是把所有經過.enter()過濾的data綁上"rect"這個元素。
現在我們所有在dataset裡的值都已經有了元素代表 "rect"。 
所以如果我們之後再用 _.enter()_ 的話， _.enter()_ 就會過濾掉我們所有dataset。
懂了嗎？

```javascript
svg.selectAll("rect")
         .data(dataset)
         .enter()
         .append("rect")
```
所以這四句簡單來說就是:
&emsp;1.先選擇我們**未來**要加到html檔上的"rect"
&emsp;2.跟D3說我們要用的data是我們已經宣告的dataset array
&emsp;3.過濾掉已經有元素代表的data值，然後用沒被過濾掉的data值執行以下指令。因為我們的dataset還沒有任何元素代表所以不會被過濾掉。
&emsp;4.將我們所有dataset裏的值都綁上"rect"這個元素。

不懂的話，建議把這頁多看幾遍。因為這是D3重要的技巧。

確定弄懂之後繼續加入:

```javascript
svg.selectAll("rect")
         .data(dataset)
         .enter()
         .append("rect")
         .attr("x", function(d, i) {
            return i * (svg_width / dataset.length);
         })
         .attr("y", function(d) {
            return svg_height - (d * 4);
         })
```
記得我們上面說 _enter()_ 過濾之後的data值都會被執行9次嗎？ (dataset裡共9個data值)
而且每次執行時候會運用一個dataset裡面的值。
所以簡單來說，dataset裏的每一個值都會執行:

```javascript
.attr("x", function(d, i) {
  return i * (svg_width / dataset.length);
})
.attr("y", function(d) {
  return svg_height - (d * 4);
})
```
OK，那attr(attribute屬性) "x" 跟 "y" 又是什麼呢？
答案是x跟y的座標，也就是說每個data值綁上的長方形的座標。

```javascript
var dataset = [ 30, 20, 10, 40, 45 , 25, 15, 35 , 18];
```
我們現在在設定每個data值的長方形的座標。
先假設我們現在在跑data值 30(dataset中的第一個)。

```javascript
.attr("x", function(d, i) {
  return i * (svg_width / dataset.length);
})
```
執行值30的時候會變成:

```javascript
.attr("x", function(30, 0) {
  return 0 * (500 / 9);
})
```
代數(variable)的變化為:

```js
d = 30
i = 0
svg_width = 500
dataset.length = 9
```
因為d代表著被執行的data值，也就是30。
i 代表著dataset array 的元素指數。因為30是array第一個，所以是 0。
svg_width 跟 dataset.length 應該就不用再解釋了。

所以，當我們跑30這個值的時候，這個值的長方形的x座標會是 0。 
0 * (500 / 9) = 0

屬性(attribute) y 也是同樣道理。

```javascript
.attr("y", function(d) {
  return svg_height - (d * 4);
})
```
執行值30的時候會變成:

```javascript
.attr("y", function(30) {
  return svg_height - (30 * 4);
})
```
svg_height 是200，所以 y = 200 -120 = 80。
這裏要先解釋一下D3對height的理解有點不一樣。

<img src="/chapters/ch3/img/height.png" alt="..." style= "max-height:150px" class="img-thumbnail">

D3對height(高度)的理解是最頂端為 0，依圖所示。
Height越高代表離svg上方界線越遠。
Width(寬度)則是和常理相同。

總和言之，我們值 30 所綁上的長方形(rect)會出現在svg上的座標(0, 80)。
而dataset裏的每個值都會執行一樣的指令來設定每個值的長方形座標。

呼～ 喘口氣，關關難過關關過。

接下來輸入:

```javascript
svg.selectAll("rect")
         .data(dataset)
         .enter()
         .append("rect")
         .attr("x", function(d, i) {
            return i * (svg_width / dataset.length);
         })
         .attr("y", function(d) {
            return svg_height - (d * 4);
         })
         .attr("width", svg_width / dataset.length)
         .attr("height", function(d) {
            return d * 4;
         })
```
主要是這兩個新的code:

```javascript
.attr("width", svg_width / dataset.length)
.attr("height", function(d) {
  return d * 4;
})
```
設定完每個值的長方形的座標之後，我們必須要設定他們的大小。
這兩個屬性其實非常好懂，顧名思義就是長方形的長寬。
Width = 寬，Height = 長。
也就是說，我們的每個值的長方形都是 500/9 = 55.55 px (畫素)
而長度就因data值而異。
跟我們在設定座標是同樣道理。
假如值是30:

```javascript
.attr("width", svg_width / dataset.length)
.attr("height", function(d) {
  return d * 4;
})
```
會變成:

```javascript
.attr("width", 500 / 9)
.attr("height", function(30) {
  return 30 * 4;
})
```
最終data值30的長方形，加上之前的x和y座標屬性，就會是一個在座標 (0, 80) 寬約55.5px和長120px的長方形。

現在就是見證奇蹟的時刻，寫了這麼久個程式碼 (其實也才不過20幾行) 終於可以按下瀏覽器的重新整理按鈕！

<img src="/chapters/ch3/img/first_draft.png" alt="..." style= "max-height:300px" class="img-thumbnail">

看到長方形了嗎？那些就是我們加在html文件上綁著data值的長方形！
雖然現在看起來還不是很起眼，不過醜小鴨也需要一點時間變天鵝。
讓我們幫它上一點美麗的色彩！

在 height 屬性之後加入 fill 這個屬性: 

```javascript
//continue...
.attr("height", function(d) {
  return d * 4;
})
.attr("fill", function(d) {
  return "rgb(" +  d*5 + ",0 ,0 )";
});
```

燈燈燈燈～ 我們的長方形進化了～ 

<img src="/chapters/ch3/img/second_draft.png" alt="..." style= "max-height:300px" class="img-thumbnail">

我們先花一點時間說一下 fill 這個屬性。這個屬性其實就是決定元素(rect)顏色的屬性。
而我們在這邊用的是rgb顏色。

```javascript
.attr("fill", function(d) {
  return "rgb(" +  d*5 + ",0 ,0 )";
});
```
因為 d 為代數，所以當data值越高的時候顏色會越紅。
有沒有發現值45的長方形最紅？

我們的紅色長方形都擠在一起視覺上不太舒適。
我們可以做一些微調，讓他們之間有些空隙。

先在之前的代數 svg_height 之後宣告一個我們間隔要用的值(bar\_patting):

```javascript
var svg_width = 500;
var svg_height = 200;
var bar_padding = 5;
```
然後在屬性長方形width的地方改成這樣:

```javascript
.attr("width", svg_width / dataset.length - bar_padding)
```
也就是讓我們的長方形中間都間隔兩個 bar-padding 的值。

按下重新整理～

<img src="/chapters/ch3/img/padding.png" alt="..." style= "max-height:300px" class="img-thumbnail">


如果你是第一次做D3，到目前為止都理解的話，代表你很有潛力。
喝杯咖啡上個廁所，我們快要完成了！

現在我們有了許多長方形，但我們卻不知道每個長方形的data值為多少。
所以接下來我們必須在每個長方形上加上數字，讓我們的圖表更簡單易懂。

用我們增加長方形的相同語法，在 svg.selectAll("rect") 那一段code**之後加上:

```javascript
//svg.selectAll("rect") 
  //那一大段code...

svg.selectAll("text")
   .data(dataset)
   .enter()
   .append("text")
```
新增的這一段跟我們增加長方形的方法一樣。
先對 "text" 元素做一個empty selection，因為我們html上沒有還沒有任何 text 元素。
宣告我們要用的 data 是我們的 dataset array。
用 _.enter()_ 過濾的已經有 text 元素代表的 data值，但因為所有在 dataset 裡的 data 值都沒有 "text" 這個元素代表 (只有我們綁上的 "rect" 元素)。所以全部 9 個 data 值都不會被過濾掉。
然後再將過濾過的 data 值都綁上 "text" 元素。
之後加上:

```javascript
.text(function(d) {
  return d;
})
```
這個程式碼會告訴D3我們要顯示什麼文字。因為我們要顯示的是 data 值，所以用 return d。
d一樣代表著被執行的data值跟上段增加長方形原理相同。
然後輸入:

```javascript
.attr("x", function(d, i) {
  return i * (svg_width / dataset.length) + (svg_width / dataset.length  - bar_padding) / 2;
})
.attr("y", function(d) {
  return svg_height - (d * 4) + 20;
})
```
這兩段設定 x 跟 y 屬性的code，跟我們設定我們長方形的 x 跟 y 座標相同。
以上 3 段 code 如果用 data 值 30 執行的話會是:

```javascript
.text(function(30) {
  return 30;
})
.attr("x", function(30, 0) {
  return 0 * (500 / 9) + (500 / 9 - 5 ) / 2;
})
.attr("y", function(d) {
  return 200 - (30 * 4) + 20;
})
```
大家可以試著套用每一個 data 值和條條看 x 跟 y 的 return 值來抓到 D3 對座標的理解。
按下重新整理。

<img src="/chapters/ch3/img/text_without_padding.png" alt="..." style= "max-height:300px" class="img-thumbnail">

看到我們在長方形上的每一個 text 都往右邊歪嗎？
所以我們要加上:

```javascript
.attr("text-anchor", "middle")
.attr("x", function(d, i) {
  return i * (svg_width / dataset.length) + (svg_width / dataset.length - bar_padding) / 2;
})
```
加在 x 屬性的上面。
重新整理。

<img src="/chapters/ch3/img/text_middle.png" alt="..." style= "max-height:300px" class="img-thumbnail">

文字調整到中間了！
最後再加上一點美化的屬性。
整段的 code 最終為:

```javascript
svg.selectAll("text")
     .data(dataset)
     .enter()
     .append("text")
     .text(function(d) {
        return d;
     })
     .attr("text-anchor", "middle")
     .attr("x", function(d, i) {
        return i * (svg_width / dataset.length) + (svg_width / dataset.length - bar_padding) / 2;
     })
     .attr("y", function(d) {
        return svg_height - (d * 4) + 20;
     })
     .attr("font-family", "sans-serif")
     .attr("font-size", "20px")
     .attr("fill", "white");
```
稍微解釋一下，"font-family" 這個屬性會宣告我們要什麼樣的字體。
"font-size" 就是字體大小。
最後 "fill"，就是字體顏色，跟長方形的顏色屬性一樣。

重新整理～最後一次。

<img src="/chapters/ch3/img/product.png" alt="..." style= "max-height:300px" class="img-thumbnail">

我們完成了簡易的長條圖！
如果有任何不懂的地方，建議把本章多看幾次。因為本章所使用的都是D3基本技巧，如果現在沒弄懂，以後只會越來愈複雜。


<a href="/chapters/ch3/code/index.html" download="index"><span class = "btn btn-success">下載長條圖成品</span></a>
















