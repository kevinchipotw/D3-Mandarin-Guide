---
layout: page
title: 第四章 - 圓餅圖
permalink: /ch4/
---
***

#### 成品圖:  

<img src="/chapters/ch4/img/pie_chart_finished.png" alt="..." style= "max-height:300px" class="img-thumbnail">

<a href="/chapters/ch3/code/index.html" download="index"><span class = "btn btn-success">下載長條圖成品</span></a>

***


#### 製作步驟: 
首先照第二章的前置作業先將開一個local server執行index.html (不會的話請先詳閱第二章)
index.html的code應如下:

```html
<!-- <!DOCTYPE html>  -->
<html> 
  <meta charset="UTF-8">
  <head>
    <script src ="http://d3js.org/d3.v3.min.js"></script>
  </head>
  <body>
  	<h1>圓餅圖之資料呈現</h1>

  </body>
</html>
```

經過章節三介紹的長條圖，我們講來探討一樣非常普遍的圓餅圖。這啷裡所用到的技巧非常類似第三章裡所介紹的基本技巧，讓我們來開始吧！


記得我們所有的程式碼都必須被script tag所圍起來。這樣一來，電腦就會認知這些程式碼為 javascript 程式碼。


```html
<script type="text/javascript">
	// 以下的code...
</script>
```

如同我們在第三章所做的，我們將先設定svg之性質（如果有不瞭解的地方，請參考第三章）值得一再強調的是，D3中的svg元件可被比喻成畫中之布，若我們不把想要呈現的元件加入svg的儔範之內，那些元件是不會呈現的！有了這一個重要的觀念，讓我們來一同探索吧！

如同之前我們所做的，我們先設定svg元件的寬度和高度以及一個稱為radius的變數：

```javascript
var svg_width = 500;
var svg_height= 200;
var radius = Math.min(svg_width, svg_height) / 2;
```

radius變數指向一個數值物件。這個數值物件利用javascript之中Math.min()之方法來取得svg_width和svg_height兩數之中的較低數來處以二。
我們將利用之前用過的好用數據：

```javascript
var dataset = [ 30, 20, 10, 40, 45 , 25, 15, 35 , 18];
```

不過目前為止，我們還未真正的建立我們後會用到的svg元件，我們目前為只只有創造了三個便數。還記得javascript這個語言是一種物件導向之程式設計語言，所以我們在此所做的事創造了三個物件，一個稱為svg_width之物件指向500之數值，另一個稱為svg_height之物件指向200之數職，而最後一稱為dataset之物件指向一個陣列為[ 30, 20, 10, 40, 45 , 25, 15, 35 , 18]。

有了這個物件導向之程式設計觀，我們接下來會來創造我們討論許久的svg元件。如以下我們所做的：


```javascript
var svg = d3.select("body")
	.append("svg")
	.attr("width", svg_width)
	.attr("height", svg_height);
```

這段程式碼應該看起來很眼熟吧？因為我們在第三章也用了這段完全一樣的程式碼。如果有疑問，請參考第三章。大致上來說，我們在此所做的是創造了一個稱為svg之變數（和之前所做的一樣）。接著我們我們把這一個剛創造的svg變數透過D3所提供的方法

```javascript
	d3.select()
```

 來指定我們HTML檔案之中稱為"body"的物件。當然在我們的HTML檔案中只有一個稱為”body"的物件，所以svg指向的物件即是我們的“body"元件。接著，我們利用著一行程式碼：

 ˋˋˋjavascript
	.append("svg")
 ˋˋˋ

 來創造一個稱為svg之物件然後將此附加到我我們前一行所指定的body物件。這個svg變數存在的目的是為了提供我們“一塊布”讓我們能夠把想要呈現的物件加入並加以呈現。接著，我們利用.attr為這個svg物件設定它的高和寬屬性，在第一個參數中我們指定我們要改變之屬性接著在第二個參數我們把我們想設定的值輸入來。在此，我們用之前所創造的svg_width和svg_height之變數來設定svg物件之屬性。

 接著我們輸入：
 ˋˋˋjavscript 
var pie = d3.layout.pie() 

var colors = d3.scale.category10(); 

var arc = d3.svg.arc() 
		.innerRadius(radius - 70)
		.outerRadius(radius - 20); 
ˋˋˋ

D3是一個既懂得人性懶散又貼心之組織架構。它提供了許多的頁面佈局(layout)，使得使用者不用靠自己計算出一些很不友善的數值來自行設定佈局。這也是為什麼D3如此之強大。它使我們的數據呈現簡化的非常，非常多。以下是D3所提供的各種頁面佈局: 

<ol> 
	<li>Pie Layout</li>
	<li>Stack Layout</li>
	<li>Tree Layout</li>
	<li>Force Layout</li>
	<li>Bundle Layout</li>
	<li>Cluster Layout</li>
	<li>Chord Layout</li>
	<li>Histogram Layout</li>
	<li>Pack Layout</li>
	<li>Partition Layout</li>
</ol>  

以上的頁面佈局之中，前三個為最常見的。而我們在之後也會一同探討這三個頁面佈局。當然因為我們在這章中所討論的是圓餅圖之數據呈現，所以我們要用的頁面設計亦即上述第一個頁面設計的圓餅頁面。以下是我們如何引進圓餅頁面之方法：

ˋˋˋjavascript
var pie = d3.layout.pie() 
ˋˋˋ

我們也引進D3貼心提供的d3.scale.category()之物件，裡面包括許多顏色以供我們的圓餅圖所使用。我們輸入：

ˋˋˋjavascript 
var colors = d3.scale.category10(); 
ˋˋˋ

來創造colors之物件並將它指向d3.scale.category10()之物件。
接著，我們又託了D3的福來引進一個稱為d3.svg.arc()之物件。這個物件是非常強大的。它使我們製造圓餅圖的過程簡單只要提供兩個為內弧形半徑innerRadius以及外弧形半徑outerRadius之值，D3自動會提供我們的圓餅圖所需的內弧形和外弧形所需的座標來呈現我們的圖。 

ˋˋˋjavascript 
var arc = d3.svg.arc() 
	.innerRadius(0)
	.outerRadius(radius - 20); 
ˋˋˋ

就是這麼的簡單！我們引進d3.svg.arc()後，我們分別把內弧形半徑innerRadius和外弧形半徑outerRadius之值設定為零和我們之前定義的radius變數減去20px。

現在我們將正式創造圓餅圖然後把它加入到我們的“布”，亦即我們的svg物件，上。

ˋˋˋjavascript
var arcs = svg.selectAll("g.arc")
	.data(pie(dataset))
	.enter() 
	.append("g")
	.attr("class", "arc") 
	.attr("transform", "translate(" + svg_width / 2 + ", " + svg_height / 2 + ")"); 
ˋˋˋ

之前已有解釋此段程式碼，但是因為D3怪異的“先預先指定物件在創造那些被指定的物件”，這一段程式碼值得我們一再回顧。簡單來說：
&emsp;1.
ˋˋˋjavascript
var arcs = svg.selectAll("g.arc")
ˋˋˋ

我們先指定了我們即將加到svg上的物件，在此為一個稱為"g"的物件中擁有"class"屬性並其值為“arc"的物件，亦即我們圓餅圖所有組成
圓頂圖的弧形。

”." javascript之用法：
	如果您以前有學過HTML和CSS,想必您應該還記得在CSS中指定特定HTML物件的方法吧？在D3中指定物件的方法類似於前者。利用“."，我們可以取出一個物件中的屬性。在這裡，”g"
	是我們要進入的物件而"arc"是我們要取出之物件的特徵。所以我們輸入的這一行程式碼：


是利用D3所提供的svg.selectAll方法把在“g"這個物件裡舉有
”class"為“arc"的物件取出並把arc變數指向這些取出之物件。但是，靈機的你們一定看到端倪吧？我們從頭到尾未曾嚐造過一個稱為"g"之物件。是的，這就至詭異之處。我們所指定的東西不
從在！這也就是我們在接下來的幾行所要做的事：創造這一些物件！

&emsp;2.
ˋˋˋjavascript
	.data(pie(dataset))
		.enter() 
		.append("g")
		.attr("class", "arc") 
ˋˋˋ

在這幾行中有很多事情發生。第一，我們把我們的資料dataset變數傳進pie()這個方法。還記
得我們之前設定把pie這一個變數指定到d3.layout.pie()嗎？這代表我們傳入的參數dataset
，其實是被傳入pie所指向的d3.layout.pie()方法。d3.layout.pie()接著會把這些資料
以圓餅頁面的形式算出複雜的x和y座標以共我們繪製圓餅圖。如果我們可以用Google Chrome
瀏覽器提供的Inspect Element(在頁面上按下右鍵最後一個選項)之console部分，來查看
d3.layout.pie()所做的事。

<img src="/img/pie_dataset.png" alt="pie_dataset" style= "max-height:150px" class="img-thumbnail">

我們把這一些D3幫我們處理的資料利用.data()方法來把這些數據“綁“在我們即將創造的物件。我們著利用.enter()方法來創造新物件
（不懂請參考第三章）。我所創造每件物件會附加一個”g"物件以及所有物件的"class"屬性會
被指定為“arc"之值。

所以，我們現在的arcs變數將是以下所呈現的：

<img src="/img/arcs_data.png" alt="arcs_data" style= "max-height:150px" class="img-thumbnail">


&emsp;3.
ˋˋˋjavascript 
	.attr("transform", "translate(" + svg_width / 2 + ",
		" + svg_height / 2 + ")"); 
ˋˋˋ

接下來來，我們將來設定我們圓餅圖之中心。因為我們想把圓餅圖顯示於我們svg物件的正中心，
所以我們將把我們所創造的所有arcs物件從原本預設值（svg元件預設的座標（0, 0)為左上角）
往-y方向移動 svg_height / 2, svg物件高度之值除以二然後往+x方向移動svg_width / 2,svg物件寬度之值除以二。這樣一來，我們原本創造以座標（0, 0) 為中心的圓餅圖會改而以
座標（svg_width / 2, svg_height / 2) 為新座標，我們的圓餅圖才會被完全顯示
在svg物件之上


呼～
經過這麼多的調整，我們已經把我們想呈現的圓餅圖設下一個良好的基礎。但是，我們並未完成全部的工作。在一下，就可以大功告成了啊！

接下來，有了我們之前所設定的弧形，內弧形半徑，以及外弧形半徑，我們只要加入顏色我們的圖就會顯示。

請輸入：

ˋˋˋjavascript
	arcs.append("path") 
		.attr("fill", function(d, i) { 
			return colors(i); 
		})
		.attr("d", arc);
ˋˋˋ

在這幾行之間，我們看到許多我們之前已經討論過的元件。首先，我們用.append來把一個稱為
path之物件加在我們的arcs物件上。接著，我們為這個path物件來加上一些屬性。還記得我們
之前有打上這行程式碼嗎？

ˋˋˋjavascript 
var colors = d3.scale.category10(); 
ˋˋˋ

現在正是我們用上這些我們預先創造的顏色物件！
我們利用一個無名函示(anonymous function) 

ˋˋˋjavascript 
		.attr("fill", function(d, i) { 
			return colors(i); 
ˋˋˋ

來將我們數據的索引數值,i,當作一個參數傳入。當這個無名函示接收到i之值，他會傳回由d3.scale.category()方法所傳回的物件，此物件就是用來為我們的圓餅圖上色的顏色。
接下來，我們又加以設定另一個稱為"d"的屬性。

ˋˋˋjavascript 
		.attr("d", arc);
ˋˋˋ

此屬性是我們剛才創造的顏色物件要涵蓋的區域。我們將這個區域設定成我們之前在

ˋˋˋjavascript 
var arc = d3.svg.arc() 
	.innerRadius(0)
	.outerRadius(radius - 20); 	
ˋˋˋ

所設定的“arc”變數。當然我們不知道他實際的值，因為這些值都是由D3提供我們的。這也是為什麼D3如此好用之其中一處。

到這裡如果您有不清楚的地方，請回去再讀一遍。不要擔心，你的努力會被賞賜的！
如果您瞭解上述所說的全部內容，恭喜！您已經在前往成為D3專家的路上跨出一大步了！

我們再加上一些數字讓讀者知道每一部分的圓餅圖真正的數值為多少。
請輸入：

ˋˋˋjavascript
arcs.append("text") 
	.attr("transform", function(d) {
		return "translate(" + arc.centroid(d) + ")";
	})
	.attr("text-anchor", "middle")
	.text(function(d) { 
		return d.value; 
	});
ˋˋˋ

我們創造了一個稱為"text"的物件然後把它加到"arcs"物件之上。接著，我們給予這個"text"物件一些屬性。首先，我們給了"transform"屬性:

ˋˋˋjavascript 
.attr("transform", function(d) {
		return "translate(" + arc.centroid(d) + ")";
	})
ˋˋˋ

我們把數據當成一個無名函示的參數。該函示傳回的值是經過arc.centroid()之方法後的結果
，亦即D3幫我們計算的(x,y)座標位於arc的正中心。接著我們加上"middle"為“text-anchor"屬性的值。最後，我們把要顯示的文字用"text"屬性來設定。其值設定為一個無名函示所傳回的值，亦即我們數據各項之值。


如果我們想把我們圓餅圖變成一個”甜甜圈圖“，別擔心！因為，我們只需要更改一行程式碼！

把：
ˋˋˋjavascript 
.innerRadius(0)
ˋˋˋ


ˋˋˋjavascript 
.innerRadius(radius - 70)
ˋˋˋ

即可取得我們想要的甜甜圈圖！注意，我們之前所設的所有文字都自動更改到我們心弧形的中心！
真的是非常，非常方便！第二張在此告一個段落，如果您對D3的強大功能深深被吸引，那麼相信您一定在未來幾章會更有收穫喔！


























