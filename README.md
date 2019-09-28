# SVGs
Scalable Vector Graphics (SVG) is a standardised graphics rendering format based on XML, which is a superset of HTML.
><svg>
  <rect x="0" y="0" width="100" height="50"/>
  <circle cx="100" cy="25" r="20" fill="red"/>
  <polygon points="200,100 250,50, 300,300 0,3">
 </svg>
 <p>SVG，指可缩放矢量图形（Scalable Vector Graphics），是用于描述二维矢量图形的一种图形格式，是由万维网联盟制定的开放标准。SVG 使用 XML 格式来定义图形，除了 IE8 之前的版本外，绝大部分浏览器都支持 SVG，可将 SVG 文本直接嵌入 HTML 中显示。
SVG 有如下特点：</p>
<li>
SVG 绘制的是矢量图，因此对图像进行放大不会失真。</li>
<li>基于 XML，可以为每个元素添加 JavaScript 事件处理器。</li>
<li>每个图形均视为对象，更改对象的属性，图形也会改变。</li>
<li>不适合游戏应用。
</li>

<h>
# D3 Basic
**D3 is a set of objects, functions, and other good stuff** 
that comes in the form of a third-party JavaScript file in the script tag. \
D3 relies on attaching itself to some HTML element, such as a div
## 1. 选择元素
在 D3 中，用于选择元素的函数有两个：
<li>d3.select()：是选择所有指定元素的第一个</li>
<li>d3.selectAll()：是选择指定元素的全部</li>

这两个函数返回的结果称为***选择集***。
使用 d3.select() 或 d3.selectAll() 选择元素后返回的对象，就是选择集。

eg.\
var body = d3.select("body"); //选择文档中的body元素 

var p1 = body.select("p")；\
p1.style("color","red");  //选择body中的第一个p元素, 改变元素颜色 

var p = body.selectAll("p");    
p.style("color","red");  //选择body中的所有p元素, 改变元素颜色

var svg = body.select("svg");   //选择body中的svg元素 \
var rects = svg.selectAll("rect");  //选择svg中所有的svg元素

`<p id="myid">Pear</p>` \
var p2 = body.select("#myid"); \
p2.style("color","red"); //使用id来选择body中第二个p元素，并改变颜色

`<p class="myclass">Pear</p>`
`<p class="myclass">Banana</p>` \
var p = body.selectAll(".myclass");\
p.style("color","red"); //使用class来选择body中第二和第三个p元素，并改变颜色

## 2. 绑定元素
D3 有一个很独特的功能：能将数据绑定到 DOM 上，也就是绑定到文档上。
例如网页中有段落元素 和一个整数 5，于是可以将整数 5 与 绑定到一起。
绑定之后，当需要依靠这个数据才操作元素的时候，会很方便。

<li>datum( ): 绑定一个数据到选择集上</li>
<li>data( )：绑定一个数组到选择集上</li>

eg1.绑定一个数据

>`<p>Apple</p>`
>`<p>Pear</p>`
>`<p>Banana</p>`
> var str = "China";

> var body = d3.select("body");\
> var p = body.selectAll("p"); \
> p.datum(str); \
> p.text(function(d, i){ return "第 "+ i + " 个元素绑定的数据是 " + d;
});

返回的结果是：

第 0 个元素绑定的数据是 China
 
第 1 个元素绑定的数据是 China
 
第 2 个元素绑定的数据是 China

---

eg2. 绑定一个数组
>`<p>Apple</p>`
>`<p>Pear</p>`
>`<p>Banana</p>` 

> var dataset = ["I like dogs","I like cats","I like snakes"];\
> var body = d3.select ("body");\
> var p = body.selectAll ("p");\
> p.data(dataset)
>  .text(function(d,i){
>       return d;
>       });

返回的结果是：

I like dogs

I like cats

I like snakes

## 3. 插入元素
插入元素涉及两个函数：
<li>append(): 在选择集末尾插入函数</li>
<li>insert(): 在选择集前插入函数</li>

\
eg1. 在选择集body 的末尾添加一个 p 元素，并将其内容设置为append an p element
> var body = d3.select("body");\
> body.append("p")\
>     .text("append an p element");

eg2. 在选择集body中id为#myid的元素前添加一个元素
> var body = d3.select("body");\
> body.insert("p", "#myid")\
>     .text("append an p element");

## 4. 删除元素
> var p = body.select("#myid");\
> p.remove();

## 5. 绘制图形或图表
D3 虽然没有明文规定一定要在 SVG 中绘图，但是 D3 提供了众多的 SVG 图形的生成器，
它们都是只支持 SVG 的。因此，建议使用 SVG 画布。 使用 D3 在 body 元素中添加 svg 的代码如下：

> var width = 300;  //画布的宽度 \
> var height = 300;   //画布的高度 \
> var svg = d3.select("body")     //选择文档中的body元素 \
>    .append("svg")          //在body中添加一个svg元素 \
>    .attr("width", width)       //设定宽度 \
>    .attr("height", height);    //设定高度