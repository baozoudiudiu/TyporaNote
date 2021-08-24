## 	圆角效果 border-radius

**border-radius**是向元素添加圆角边框。

**使用方法：**

**border-radius:10px;** /* 所有角都使用半径为10px的圆角 */ 

[![img](http://img.mukewang.com/52e216d2000195ef01110111.jpg)](http://img.mukewang.com/52e216d2000195ef01110111.jpg)

**border-radius: 5px 4px 3px 2px;** /* 四个半径值分别是左上角、右上角、右下角和左下角，顺时针 */ 

[![img](http://img.mukewang.com/52e216f9000131a201110111.jpg)](http://img.mukewang.com/52e216f9000131a201110111.jpg)

不要以为border-radius的值只能用**px**单位，你还可以用**百分比**或者**em**，但兼容性目前还不太好。

**实心上半圆：**

方法：把高度(height)设为宽度（width）的一半，并且只设置左上角和右上角的半径与元素的高度一致（大于也是可以的）。

```
div{
    height:50px;/*是width的一半*/
    width:100px;
    background:#9da;
    border-radius:50px 50px 0 0;/*半径至少设置为height的值*/
    }
```

**实心圆：**
方法：把宽度（width）与高度(height)值设置为一致（也就是正方形），并且四个圆角值都设置为它们值的一半。如下代码：

```
div{
    height:100px;/*与width设置一致*/
    width:100px;
    background:#9da;
    border-radius:50px;/*四个圆角值都设置为宽度或高度值的一半*/
    }
```

## 阴影

> box-shadow: X轴偏移量 Y轴偏移量 [阴影模糊半径] [阴影扩展半径] [阴影颜色] [投影方式];
>
> 阴影模糊半径：此参数可选，其值只能是为正值，如果其值为0时，表示阴影不具有模糊效果，其值越大阴影的边缘就越模糊；
>
> 阴影扩展半径：此参数可选，其值可以是正负值，如果值为正，则整个阴影都延展扩大，反之值为负值时，则缩小；

```html
<!doctype html>
<html>
<head>
<meta charset="utf-8">
<title>boxshadow</title>
<style>
.boxshadow-outset{
    width:100px;
	height:100px;
    box-shadow:4px 4px 6px #666; 
}
.boxshadow-inset{
    width:100px;
    height:100px;
    box-shadow:4px 4px 6px #666 inset; 
}
.boxshadow-multi{
    width:100px;
    height:100px;
    box-shadow:4px 2px 6px #f00, -4px -2px 6px #000, 0px 0px 12px 5px #33CC00 inset;
}

</style>
</head>

<body>
<h2>外阴影</h2>
<div class="boxshadow-outset">
</div>
<br />
<h2>内阴影</h2>
<div class="boxshadow-inset">
</div>
<br />
<h2>多阴影</h2>
<div class="boxshadow-multi">
</div>
</body>CSS3边框  
</html>
```

## 边框图片

```html
<!doctype html>
<html>
<head>
<meta charset="utf-8">
<title>边框图片</title>
<style>
#border_image {
  margin:0 auto;
	height:100px;
	line-height:100px;
	text-align:center;
	font-size:30px;
	width:450px;
	border:15px solid #ccc;
  border-image:url(http://img.mukewang.com/52e22a1c0001406e03040221.jpg) 70 repeat;
  /* round (平铺)，repeat（重复），stretch（拉伸）*/
	}
</style>
</head>
<body>
<div id="border_image">
请为我镶嵌上漂亮的画框吧
</div>
</body>
</html>
```

## 渐变色

```html
<!DOCTYPE html>
<html>
<head> 
<meta charset="utf-8">
<title>Gradient</title>
<style type="text/css">

p {
  width: 400px;
  height: 150px;
  line-height: 150px;
  text-align:center;
  color: #000;
  font-size:24px;
  background-image:linear-gradient(to left, red, orange, yellow, green, blue, indigo, violet);
  /* to left（从右向左）*/
  /* to right（从左向右）*/
  /* to bottom（从上到下）*/
  /* to top（从下到上）*/
  /* to top left（从右下角到左上角）*/
  /* to top right（从左下角到右上角）*/
} 
</style>
</head> 
<body>
　　<p>右下角向左上角的线性渐变背景</p>
</body>
</html>
```

## 文字溢出

超出部分裁剪

```css
text-overflow: clip;
```

超出部分显示...

```css
text-overflow: ellipsis;
overflow: hidden;
white-space: nowrap;
```

## 文本阴影

text-shadow可以用来设置文本的阴影效果。

**语法：**

```css
text-shadow: X-Offset Y-Offset blur color;
```

> X-Offset：表示阴影的水平偏移距离，其值为正值时阴影向右偏移，反之向左偏移；   
>
> Y-Offset：是指阴影的垂直偏移距离，如果其值是正值时，阴影向下偏移，反之向上偏移；
>
> Blur：是指阴影的模糊程度，其值不能是负值，如果值越大，阴影越模糊，反之阴影越清晰，如果不需要阴影模糊可以将Blur值设置为0；
>
> Color：是指阴影的颜色，其可以使用rgba色。
>
> 比如，我们可以用下面代码实现设置阴影效果。

## background-origin (背景图起始位置)

设置元素背景图片的**原始起始位置**。

语法：

```css
background-origin ： border-box | padding-box | content-box;
```

参数分别表示背景图片是从**边框**，还是**内边距（默认值）**，或者是**内容区域**开始显示。

效果如下：

![img](http://img.mukewang.com/531003de0001166903660166.jpg)

**需要注意的是**，如果背景不是**no-repeat**，这个属性无效，它会从边框开始显示。

```html
<!DOCTYPE html>
<html>
<head> 
<meta charset="utf-8">
<title>背景原点</title>
<style type="text/css">
.wrap {
    width:220px; 
    border:20px dashed #000; 
    padding:20px; 
    font-weight:bold; 
    color:#000; 
    background:#ccc url(http://static.mukewang.com/static/img/logo_index.png) no-repeat; 
    background-origin: content-box;
    position: relative;
}
.wrap span { 
    position: absolute; 
    left:0; 
    top:0;
}
.content {
    height:80px; 
    border:1px solid #333;
}
</style>  
</head> 
<body>
<div class="wrap"><span>padding</span>
    <div class="content">content</div>
</div>
</body>
</html>
```

##  background-clip（背景图裁剪）

用来将背景图片做适当的**裁剪**以适应实际需要。

语法：

```css
background-clip ： border-box | padding-box | content-box | no-clip
```

参数分别表示从**边框、**或**内填充**，或者**内容区域**向外裁剪背景。**no-clip**表示不裁切，和**参数border-box**显示同样的效果。`backgroud-clip`默认值为**border-box**。

效果如下图所示：

![img](http://img.mukewang.com/5310065d0001c95103660166.jpg)

```html
<!DOCTYPE html>
<html>
<head> 
<meta charset="utf-8">
<title>背景裁切</title>
<style type="text/css">
.wrap {
    width:220px; 
    border:20px dashed #000; 
    padding:20px; 
    font-weight:bold; 
    color:#000; 
    background:#ccc url(http://static.mukewang.com/static/img/logo_index.png) no-repeat; 
    background-origin: border-box;
    background-clip: padding-box;
    position: relative;
}
.wrap span { 
    position: absolute; 
    left:0; 
    top:0;
}
.content {
    height:80px; 
    border:1px solid #333;
}
</style>  
</head> 
<body>
<div class="wrap"><span>padding</span>
    <div class="content">content</div>
</div>
</body>
</html>
```

## background-size（背景图尺寸）

设置背景图片的大小，以**长度值**或**百分比**显示，还可以通过**cover**和**contain**来对图片进行伸缩。

语法：

```css
background-size: auto | <长度值> | <百分比> | cover | contain
```

取值说明：

**1、auto**：默认值，不改变背景图片的原始高度和宽度；

**2、<长度值>**：成对出现如200px 50px，将背景图片宽高依次设置为前面两个值，当设置一个值时，将其作为图片宽度值来**等比缩放**；

**3、<百分比>**：0％~100％之间的任何值，将背景图片宽高依次设置为所在元素宽高乘以前面百分比得出的数值，当设置一个值时同上；

**4、cover**：顾名思义为**覆盖**，即将背景图片等比缩放以**填满整个容器**；

**5、contain**：容纳，即将背景图片等比缩放至**某一边紧贴容器边缘为止**。



## 属性选择器

在HTML中，通过各种各样的属性可以给元素增加很多附加的信息。例如，通过id属性可以将不同div元素进行区分。

  在CSS2中引入了一些属性选择器，而CSS3在CSS2的基础上对属性选择器进行了扩展，新增了3个属性选择器，使得属性选择器有了**通配符**的概念，这三个属性选择器与CSS2的属性选择器共同构成了CSS功能强大的属性选择器。如下表所示：

[![img](http://img.mukewang.com/56653eba0001b07004610215.jpg)](http://img.mukewang.com/56653eba0001b07004610215.jpg)

 **实例展示：**

**html代码**：

```
<a href="xxx.pdf">我链接的是PDF文件</a>
<a href="#" class="icon">我类名是icon</a>
<a href="#" title="我的title是more">我的title是more</a>
```

**css代码** 

```
a[class^=icon]{
  background: green;
  color:#fff;
}
a[href$=pdf]{
  background: orange;
  color: #fff;
}
a[title*=more]{
  background: blue;
  color: #fff;
}
```

 结果显示：

[![img](http://img.mukewang.com/53202e050001c07e03820068.jpg)](http://img.mukewang.com/53202e050001c07e03820068.jpg)

## 结构性伪类选择器—root

`:root`选择器，从字面上我们就可以很清楚的理解是根选择器，他的意思就是匹配元素E所在文档的根元素。在HTML文档中，根元素始终是<html>。

**示例演示：**

通过“:root”选择器设置背景颜色

**HTML代码：**

```
<div>:root选择器的演示</div>
```

**CSS代码：**

```
:root {
  background:orange;
}
```

**演示结果：**

![img](http://img.mukewang.com/531eb1d90001735d01560050.jpg)

“:root”选择器等同于<html>元素，简单点说：

```
:root{background:orange}
html {background:orange;}
```

得到的效果等同。

建议使用:root方法。



## 结构性伪类选择器—not

`:not`选择器称为**否定选择器**，和jQuery中的:not选择器一模一样，**可以选择除某个元素之外的所有元素**。就拿form元素来说，比如说你想给表单中**除submit按钮之外**的input元素添加红色边框，**CSS代码**可以写成：

```
form {
  width: 200px;
  margin: 20px auto;
}
div {
  margin-bottom: 20px;
}
input:not([type="submit"]){
  border:1px solid red;
}
```

**相关HTML代码：**

```
<form action="#">
  <div>
    <label for="name">Text Input:</label>
    <input type="text" name="name" id="name" placeholder="John Smith" />
  </div>
  <div>
    <label for="name">Password Input:</label>
    <input type="text" name="name" id="name" placeholder="John Smith" />
  </div>
  <div>
    <input type="submit" value="Submit" />
  </div>
</form>  
```

**演示结果：**

**![img](http://img.mukewang.com/531eb2ca00014b5002370177.jpg)**

## 结构性伪类选择器—empty

`:empty`选择器表示的就是空。用来选择没有任何内容的元素，这里没有内容指的是一点内容都没有，**哪怕是一个空格**。

示例显示：

比如说，你的文档中有三个段落p元素，你想把没有任何内容的P元素隐藏起来。我们就可以使用“:empty”选择器来控制。

**HTML代码：**

```html
<p>我是一个段落</p>
<p> </p>
<p></p>
```

**CSS代码：**

```css
p{
 background: orange;
 min-height: 30px;
}
p:empty {
  display: none;
}
```

**演示结果：**

**![img](http://img.mukewang.com/531eb55b0001d7d401580126.jpg)**



## 结构性伪类选择器—target

`:target`选择器称为目标选择器，用来匹配文档(页面)的**url的某个标志符的目标元素**。我们先来上个例子，然后再做分析。

**示例展示**

点击链接显示隐藏的段落。

**HTML代码：**

```html
<h2><a href="#brand">Brand</a></h2>
<div class="menuSection" id="brand">
    content for Brand
</div>
```

**CSS代码：**

```css
.menuSection{
  display: none;
}
:target{/*这里的:target就是指id="brand"的div对象*/
  display:block;
}
```

**演示结果：**

[![img](http://img.mukewang.com/53217ea30001103002230101.jpg)](http://img.mukewang.com/53217ea30001103002230101.jpg)

**分析：**

1、具体来说，触发元素的URL中的标志符通常会包含一个**#号**，后面带有一个**标志符名称**，上面代码中是：`#brand`

2、：target就是用来匹配id为“brand”的元素（id="brand"的元素）,上面代码中是那个div元素。

**多个url（多个target）处理：**

就像上面的例子，#brand与后面的id="brand"是对应的，当同一个页面上有很多的url的时候你可以取不同的名字，只要#号后对的名称与id=""中的名称对应就可以了。
如下面例子：
html代码：  

```html
<h2><a href="#brand">Brand</a></h2>
<div class="menuSection" id="brand">
  content for Brand
</div>
<h2><a href="#jake">Brand</a></h2>
<div class="menuSection" id="jake">
 content for jake
</div>
<h2><a href="#aron">Brand</a></h2>
<div class="menuSection" id="aron">
    content for aron
</div>
```

css代码：

```css
#brand:target {
  background: orange;
  color: #fff;
}
#jake:target {
  background: blue;
  color: #fff;
}
#aron:target {
  background: red;
  color: #fff;
}
```

上面的代码可以对不同的target对象分别设置不的样式。



## 结构性伪类选择器—first-child

“:first-child”选择器表示的是**选择父元素的第一个子元素的元素E**。简单点理解就是选择元素中的第一个子元素，记住是**子元素**，而不是后代元素。

**示例演示**

通过“:first-child”选择器定位列表中的第一个列表项，并将序列号颜色变为红色。

**HTML代码：**

```html
<ol>
  <li><a href="##">Link1</a></li>
  <li><a href="##">Link2</a></li>
  <li><a href="##">link3</a></li>
</ol>
```

**CSS代码：**

```css
ol > li{
  font-size:20px;
  font-weight: bold;
  margin-bottom: 10px;
}

ol a {
  font-size: 16px;
  font-weight: normal;
}

ol > li:first-child{
  color: red;
}
```

**演示结果：**

![img](http://img.mukewang.com/531eb8ca0001c5ba01250125.jpg)



## 结构性伪类选择器—last-child

和`first-child`使用类似，用于处理最后一个元素。



## 结构性伪类选择器—nth-child(n)

“:nth-child(n)”选择器用来定位某个**父元素**的**一个或多个特定的子元素**。其中“n”是其参数，而且可以是整数值(1,2,3,4)，也可以是表达式(2n+1、-n+5)和关键词(odd、even)，但参数n的起始值始终是1，而不是0。也就是说，参数n的值为0时，选择器将选择不到任何匹配的元素。

**经验与技巧:**当“:nth-child(n)”选择器中的n为一个表达式时，其中n是从0开始计算，当表达式的值为0或小于0的时候，不选择任何匹配的元素。如下表所示：

![img](http://img.mukewang.com/531eba56000138aa05870197.jpg)

**案例演示**

 通过“:nth-child(n)”选择器，并且参数使用表达式“2n”，将偶数行列表背景色设置为橙色。

**HTML代码：**

```html
<ol>
  <li>item1</li>
  <li>item2</li>
  <li>item3</li>
  <li>item4</li>
  <li>item5</li>
  <li>item6</li>
  <li>item7</li>
  <li>item8</li>
  <li>item9</li>
  <li>item10</li>
</ol>
```

**CSS代码：**

```css
ol > li:nth-child(2n){
  background: orange;
}
```

**演示结果：
![img](http://img.mukewang.com/531ebac90001750902580228.jpg)**

## 结构性伪类选择器—nth-last-child(n)

“:nth-last-child(n)”选择器和前面的“:nth-child(n)”选择器非常的相似，只是这里多了一个“last”，所起的作用和“:nth-child(n)”选择器有所区别，从某父元素的最后一个子元素开始计算，来选择特定的元素。



## first-of-type选择器

“:first-of-type”选择器类似于“:first-child”选择器，不同之处就是**指定了元素的类型**,其主要用来定位一个父元素下的某个类型的第一个子元素。

**示例演示：**

通过“:first-of-type”选择器，定位div容器中的第一个p元素（p不一定是容器中的第一个子元素），并设置其背景色为橙色。

**HTML代码：**

```html
<div class="wrapper">
  <div>我是一个块元素，我是.wrapper的第一个子元素</div>
  <p>我是一个段落元素，我是不是.wrapper的第一个子元素，但是他的第一个段落元素</p>
  <p>我是一个段落元素</p>
  <div>我是一个块元素</div>
</div>
```

**CSS代码：**

```css
.wrapper {
  width: 500px;
  margin: 20px auto;
  padding: 10px;
  border: 1px solid #ccc;
  color: #fff;
}
.wrapper > div {
  background: green;
}
.wrapper > p {
  background: blue;
}
/*我要改变第一个段落的背景为橙色*/
.wrapper > p:first-of-type {
  background: orange;
}
```

演示结果：

![img](http://img.mukewang.com/532959820001ab6804700149.jpg)



## nth-of-type(n)选择器

“`:nth-of-type(n)`”选择器和“`:nth-child(n)`”选择器非常类似，不同的是它只计算父元素中指定的某种类型的子元素。当某个元素中的子元素不单单是同一种类型的子元素时，使用“:nth-of-type(n)”选择器来定位于父元素中某种类型的子元素是非常方便和有用的。在“:nth-of-type(n)”选择器中的“n”和“:nth-child(n)”选择器中的“n”参数也一样，可以是具体的**整数**，也可以是**表达式**，还可以是**关键词**。

**示例演示**

通过“:nth-of-type(2n)”选择器，将容器“div.wrapper”中偶数段数的背景设置为橙色。

**HTML代码：**

```html
<div class="wrapper">
  <div>我是一个Div元素</div>
  <p>我是一个段落元素</p>
  <div>我是一个Div元素</div>
  <p>我是一个段落</p>
  <div>我是一个Div元素</div>
  <p>我是一个段落</p>
  <div>我是一个Div元素</div>
  <p>我是一个段落</p>
  <div>我是一个Div元素</div>
  <p>我是一个段落</p>
  <div>我是一个Div元素</div>
  <p>我是一个段落</p>
  <div>我是一个Div元素</div>
  <p>我是一个段落</p>
  <div>我是一个Div元素</div>
  <p>我是一个段落</p>
</div>
```

**CSS代码：**

```css
.wrapper > p:nth-of-type(2n){
  background: orange;
}
```

**演示结果：**

![img](http://img.mukewang.com/532be1ed00010f5403290494.jpg)



## last-of-type选择器

“`:last-of-type`”选择器和“`:first-of-type`”选择器功能是一样的，不同的是他选择是父元素下的某个类型的`最后一个子元素`。



## nth-last-of-type(n)选择器

“`:nth-last-of-type(n)`”选择器和“`:nth-of-type(n)`”选择器是一样的，选择父元素中指定的某种子元素类型，但它的起始方向是从最后一个子元素开始，而且它的使用方法类似于上节中介绍的“`:nth-last-child(n)`”选择器一样。



## only-child选择器

“`:only-child`”选择器选择的是父元素中只有一个子元素，而且只有唯一的一个子元素。也就是说，匹配的元素的父元素中仅有一个子元素，而且是一个**唯一的子元素**。

**示例演示**

通过“:only-child”选择器，来控制仅有一个子元素的背景样式，为了更好的理解，我们这个示例通过对比的方式来向大家演示。

**HTML代码：**

```html
<div class="post">
  <p>我是一个段落</p>
  <p>我是一个段落</p>
</div>
<div class="post">
  <p>我是一个段落</p>
</div>
```

**CSS代码：**

```css
.post p {
  background: green;
  color: #fff;
  padding: 10px;
}
.post p:only-child {
  background: orange;
}
```

**演示结果：**

![img](http://img.mukewang.com/53295d4a0001e07202260173.jpg)



## only-of-type选择器

`“:only-of-type”`选择器用来选择一个元素是它的父元素的唯一一个相同类型的子元素。这样说或许不太好理解，换一种说法。`“:only-of-type”`是表示一个元素他有很多个子元素，而其中只有一种类型的子元素是唯一的，使用“:only-of-type”选择器就可以选中这个元素中的唯一一个类型子元素。

**示例演示**

通过“:only-of-type”选择器来修改容器中仅有一个div元素的背景色为橙色。

**HTML代码：**

```html
<div class="wrapper">
  <p>我是一个段落</p>
  <p>我是一个段落</p>
  <p>我是一个段落</p>
  <div>我是一个Div元素</div>
</div>
<div class="wrapper">
  <div>我是一个Div</div>
  <ul>
    <li>我是一个列表项</li>
  </ul>
  <p>我是一个段落</p>
</div>
```

**CSS代码：**

```css
.wrapper > div:only-of-type {
  background: orange;
}
```

**演示结果：**

![img](http://img.mukewang.com/53295deb000128d801980212.jpg)



## :enabled选择器

在Web的表单中，有些表单元素有可用（**“:enabled”**）和不可用（“**:disabled**”）状态，比如输入框，密码框，复选框等。在默认情况之下，这些表单元素都处在可用状态。那么我们可以通过伪选择器“**:enabled**”对这些表单元素设置样式。

**示例演示**

通过“:enabled”选择器，修改文本输入框的边框为2像素的红色边框，并设置它的背景为**灰色**。

**HTML代码:**

```html
<form action="#">
  <div>
    <label for="name">Text Input:</label>
    <input type="text" name="name" id="name" placeholder="可用输入框"  />
  </div>
   <div>
    <label for="name">Text Input:</label>
    <input type="text" name="name" id="name" placeholder="禁用输入框"  disabled="disabled" />
  </div>
</form>  
```

**CSS代码：**

```css
div{
  margin: 20px;
}
input[type="text"]:enabled {
  background: #ccc;
  border: 2px solid red;
}
```

**结果演示**

![img](http://img.mukewang.com/5335299700015e3403000084.jpg)

## :disabled选择器

“**:disabled**”选择器刚好与“**:enabled**”选择器相反，用来选择不可用表单元素。要正常使用“:disabled”选择器，需要在表单元素的HTML中设置“disabled”属性。



## :checked选择器

在表单元素中，单选按钮和复选按钮都具有**选中**和**未选中**状态。（大家都知道，要覆写这两个按钮默认样式比较困难）。在CSS3中，我们可以通过状态选择器“:checked”配合其他标签实现**自定义样式**。而“**:checked**”表示的是选中状态。

**示例演示：**

通过“:checked”状态来自定义复选框效果。

**HTML代码**

```
<form action="#">
  <div class="wrapper">
    <div class="box">
      <input type="checkbox" checked="checked" id="usename" /><span>√</span>
    </div>
    <lable for="usename">我是选中状态</lable>
  </div>
  
  <div class="wrapper">
    <div class="box">
      <input type="checkbox"  id="usepwd" /><span>√</span>
    </div>
    <label for="usepwd">我是未选中状态</label>
  </div>
</form> 
```

**CSS代码：**

```
form {
  border: 1px solid #ccc;
  padding: 20px;
  width: 300px;
  margin: 30px auto;
}

.wrapper {
  margin-bottom: 10px;
}

.box {
  display: inline-block;
  width: 20px;
  height: 20px;
  margin-right: 10px;
  position: relative;
  border: 2px solid orange;
  vertical-align: middle;
}

.box input {
  opacity: 0;
  position: absolute;
  top:0;
  left:0;
}

.box span {
  position: absolute;
  top: -10px;
  right: 3px;
  font-size: 30px;
  font-weight: bold;
  font-family: Arial;
  -webkit-transform: rotate(30deg);
  transform: rotate(30deg);
  color: orange;
}

input[type="checkbox"] + span {
  opacity: 0;
}

input[type="checkbox"]:checked + span {
  opacity: 1;
}
```

结果演示

![img](http://img.mukewang.com/53326d1f0001b8a703280126.jpg)



## ::selection选择器

“**::selection**”伪元素是用来匹配**突出显示**的文本(用鼠标选择文本时的文本)。浏览器默认情况下，用鼠标选择网页文本是以“深蓝的背景，白色的字体”显示的，效果如下图所示：

[![img](http://img.mukewang.com/533e50910001bff808670219.jpg)](http://img.mukewang.com/533e50910001bff808670219.jpg)

从上图中可以看出，用鼠标选中“专注IT、互联网技术”、“纯干货、学以致用”、“没错、这是免费的”这三行文本中，默认显示样式为：蓝色背景、白色文本。

有的时候设计要求,不使用上图那种浏览器默认的突出文本效果，需要一个与众不同的效果，此时“**::selection**”伪元素就非常的实用。不过在**Firefox浏览器**还需要添加前缀。

**示例演示:**

通过“::selection”选择器，将Web中选中的文本背景变成红色，文本变成绿色。

**HTML代码：**

```html
<p>“::selection”伪元素是用来匹配突出显示的文本。浏览器默认情况下，选择网站文本是深蓝的背景，白色的字体，</p>
```

**CSS代码：**

```css
::-moz-selection {
  background: red;
  color: green;
}
::selection {
  background: red;
  color: green;
}
```

结果演示：

[![img](http://img.mukewang.com/533e52b80001973007260033.jpg)](http://img.mukewang.com/533e52b80001973007260033.jpg)

注意：

1、IE9+、Opera、Google Chrome 以及 Safari 中支持 ::selection 选择器。

2、Firefox 支持替代的 ::-moz-selection。



## :read-only选择器

“**:read-only**”伪类选择器用来指定处于只读状态元素的样式。简单点理解就是，元素中设置了“**readonly=’readonly’**”

**示例演示**

通过“:read-only”选择器来设置地址文本框的样式。



## :read-write选择器

“**:read-write**”选择器刚好与“**:read-only**”选择器**相反**，主要用来指定当元素处于**非只读状态**时的样式。



## ::before和::after

::before和::after这两个主要用来给元素的前面或后面插入内容，这两个常和"content"配合使用，使用的场景最多的就是清除浮动。

```css
.clearfix::before,
.clearfix::after {
    content: ".";
    display: block;
    height: 0;
    visibility: hidden;
}
.clearfix:after {clear: both;}
.clearfix {zoom: 1;}
```


当然可以利用他们制作出其他更好的效果，比如右侧中的阴影效果，也是通过这个来实现的。

关键代码分析：

```css
.effect::before, .effect::after{
    content:"";
    position:absolute;
    z-index:-1;
    -webkit-box-shadow:0 0 20px rgba(0,0,0,0.8);
    -moz-box-shadow:0 0 20px rgba(0,0,0,0.8);
    box-shadow:0 0 20px rgba(0,0,0,0.8);
    top:50%;
    bottom:0;
    left:10px;
    right:10px;
    -moz-border-radius:100px / 10px;
    border-radius:100px / 10px;
}
```

上面代码作用在class名叫.effect上的div的前（before）后(after)都添加一个空元素，然后为这两个空元素添加阴影特效。

想看这个知识点深入讲解的小伙伴请观看[《css3实现图片阴影效果》](http://www.imooc.com/learn/240)中的[第1-6小节](http://www.imooc.com/video/5865)。



## 旋转 rotate()

**旋转rotate()函数**通过指定的角度参数使元素相对原点进行旋转。它主要在二维空间内进行操作，设置一个角度值，用来指定旋转的幅度。如果这个值为**正值**，元素相对原点中心**顺时针**旋转；如果这个值为**负值**，元素相对原点中心**逆时针**旋转。如下图所示：

![img](http://img.mukewang.com/53390fc500014a6603930267.jpg)

**HTML代码：**

```
<div class="wrapper">
  <div></div>
</div>
```

**CSS代码：**

```
.wrapper {
  width: 200px;
  height: 200px;
  border: 1px dotted red;
  margin: 100px auto;
}
.wrapper div {
  width: 200px;
  height: 200px;
  background: orange;
  -webkit-transform: rotate(45deg);
  transform: rotate(45deg);
}
```

**演示结果**

**![img](http://img.mukewang.com/5339106f00018d3a04200298.jpg)**

## 扭曲 skew()

扭曲skew()函数能够让元素**倾斜显示**。它可以将一个对象以其中心位置围绕着**X轴**和**Y轴**按照一定的角度倾斜。这与rotate()函数的旋转不同，rotate()函数只是旋转，而不会改变元素的形状。skew()函数不会旋转，而只会改变元素的形状。

**Skew()具有三种情况：**

**1、skew(x,y)使元素在水平和垂直方向同时扭曲**（X轴和Y轴同时按一定的角度值进行扭曲变形）；

![img](http://img.mukewang.com/533913260001d2d003590222.jpg)

第一个参数对应X轴，第二个参数对应Y轴。如果第二个参数未提供，则值为0，也就是Y轴方向上无斜切。

**2、skewX(x)仅使元素在水平方向扭曲变形**（X轴扭曲变形）；

![img](http://img.mukewang.com/533913750001e21603680209.jpg)

**3、****skewY(y)仅使元素在垂直方向扭曲变形**（Y轴扭曲变形）

![img](http://img.mukewang.com/533913920001d78d03670208.jpg)

**示例演示：**

通过skew（）函数将长方形变成平行四边形。

**HTML代码：**

```
<div class="wrapper">
  <div>我变成平形四边形</div>
</div>
```

**CSS代码：**

```
.wrapper {
  width: 300px;
  height: 100px;
  border: 2px dotted red;
  margin: 30px auto;
}
.wrapper div {
  width: 300px;
  height: 100px;
  line-height: 100px;
  text-align: center;
  color: #fff;
  background: orange;
  -webkit-transform: skew(45deg);
  -moz-transform:skew(45deg) 
  transform:skew(45deg);
}
```

**演示结果**

**![img](http://img.mukewang.com/5339140b0001259804140145.jpg)**



## 缩放 scale()

**缩放 scale()函数** 让元素根据中心原点对对象进行缩放。

缩放 scale 具有三种情况：

**1、 scale(X,Y)使元素水平方向和垂直方向同时缩放**（也就是X轴和Y轴同时缩放）

![img](http://img.mukewang.com/53391aff000181f703520211.jpg)

例如：

```
div:hover {
  -webkit-transform: scale(1.5,0.5);
  -moz-transform:scale(1.5,0.5)
  transform: scale(1.5,0.5);
}
```

注意：Y是一个可选参数，如果没有设置Y值，则表示X，Y两个方向的缩放倍数是一样的。

**2、scaleX(x)元素仅水平方向缩放**（X轴缩放）

![img](http://img.mukewang.com/53391b0b00016a7002920170.jpg)

**3、scaleY(y)元素仅垂直方向缩放**（Y轴缩放）

![img](http://img.mukewang.com/53391b14000169cf03280183.jpg)

**HTML代码：**

```
<div class="wrapper">
  <div>我将放大1.5倍</div>
</div>
```

**CSS代码：**

```
.wrapper {
  width: 200px;
  height: 200px;
  border:2px dashed red;
  margin: 100px auto;
}
.wrapper div {
  width: 200px;
  height: 200px;
  line-height: 200px;
  background: orange;
  text-align: center;
  color: #fff;
}
.wrapper div:hover {
  opacity: .5;
  -webkit-transform: scale(1.5);
  -moz-transform:scale(1.5)
  transform: scale(1.5);
}
```

**演示结果**

![img](http://img.mukewang.com/53391b760001041803020277.jpg)

**注意：** **scale()**的取值默认的值为1，当值设置为**0.01**到**0.99**之间的任何值，作用使一个元素缩小；而任何大于或等于**1.01**的值，作用是让元素放大



## 位移 translate()

**translate()函数**可以将元素向指定的方向移动，类似于position中的**relative**。或以简单的理解为，使用translate()函数，可以把元素从原来的位置移动，而不影响在X、Y轴上的任何Web组件。

**translate我们分为三种情况：**

**1、translate(x,y)水平方向和垂直方向同时移动**（也就是X轴和Y轴同时移动）

![img](http://img.mukewang.com/53391c640001709503850257.jpg)

**2、translateX(x)仅水平方向移动**（X轴移动）

![img](http://img.mukewang.com/53391c920001420703810201.jpg)

**3、translateY(Y)仅垂直方向移动**（Y轴移动）

![img](http://img.mukewang.com/53391ca70001da5e03570211.jpg)

**实例演示：**通过translate()函数将元素向Y轴下方移动50px,X轴右方移动100px。

**HTML代码：**

```
<div class="wrapper">
  <div>我向右向下移动</div>
</div>
```

**CSS代码：**

```
.wrapper {
  width: 200px;
  height: 200px;
  border: 2px dotted red;
  margin: 20px auto;
}
.wrapper div {
  width: 200px;
  height: 200px;
  line-height: 200px;
  text-align: center;
  background: orange;
  color: #fff;
  -webkit-transform: translate(50px,100px);
  -moz-transform:translate(50px,100px);
  transform: translate(50px,100px);
}
```

**演示结果**

**![img](http://img.mukewang.com/53391d0e0001502d03410319.jpg)**



## 矩阵 matrix()

**matrix()** 是一个含六个值的(a,b,c,d,e,f)变换矩阵，用来指定一个2D变换，相当于直接应用一个[a b c d e f]变换矩阵。就是基于水平方向（X轴）和垂直方向（Y轴）重新定位元素,此属性值使用涉及到数学中的矩阵，我在这里只是简单的说一下CSS3中的transform有这么一个属性值，如果需要深入了解，需要对数学矩阵有一定的知识。

**示例演示：**通过matrix()函数来模拟transform中translate()位移的效果。
**HTML代码：**

```
<div class="wrapper">
  <div></div>
</div>
```

**CSS代码：**

```
.wrapper {
  width: 300px;
  height: 200px;
  border: 2px dotted red;
  margin: 40px auto;
}
.wrapper div {
  width:300px;
  height: 200px;
  background: orange;
  -webkit-transform: matrix(1,0,0,1,50,50);
  -moz-transform:matrix(1,0,0,1,50,50);
  transform: matrix(1,0,0,1,50,50);
}
```

**演示结果：**

**![img](http://img.mukewang.com/53391e000001b60b03890278.jpg)**



## 原点 transform-origin

任何一个元素都有一个中心点，默认情况之下，其中心点是居于元素X轴和Y轴的50%处。如下图所示：

![img](http://img.mukewang.com/53391e740001b03d03330333.jpg)

在没有重置transform-origin改变元素原点位置的情况下，CSS变形进行的旋转、位移、缩放，扭曲等操作都是**以元素自己中心位置进行变形**。但很多时候，我们可以通过transform-origin来对元素进行原点位置改变，使元素原点不在元素的中心位置，以达到需要的原点位置。

transform-origin取值和元素设置背景中的background-position取值类似，如下表所示：

![img](http://img.mukewang.com/53391ea500013e4706860384.jpg)

**示例展示：**

通过transform-origin改变元素原点到左上角，然后进行顺时旋转45度。

**HTML代码：**

```
<div class="wrapper">
  <div>原点在默认位置处</div>
</div>
<div class="wrapper transform-origin">
  <div>原点重置到左上角</div>
</div>
```

**CSS代码：**

```
.wrapper {
  width: 300px;
  height: 300px;
  float: left;
  margin: 100px;
  border: 2px dotted red;
  line-height: 300px;
  text-align: center;
}
.wrapper div {
  background: orange;
  -webkit-transform: rotate(45deg);
  transform: rotate(45deg);
}
.transform-origin div {
  -webkit-transform-origin: left top;
  transform-origin: left top;
}
```

**演示结果：**

**![img](http://img.mukewang.com/53391f030001eaa209440496.jpg)**.

## CSS3中的动画--过渡属性 transition-property

早期在Web中要实现动画效果，都是依赖于JavaScript或Flash来完成。但在CSS3中新增加了一个新的模块transition，它可以通过一些简单的CSS事件来触发元素的外观变化，让效果显得更加细腻。简单点说，**就是通过鼠标的单击、获得焦点，被点击或对元素任何改变中触发，并平滑地以动画效果改变CSS的属性值。**

```
在CSS中创建简单的过渡效果可以从以下几个步骤来实现：
第一，在默认样式中声明元素的初始状态样式；
第二，声明过渡元素最终状态样式，比如悬浮状态；
第三，在默认样式中通过添加过渡函数，添加一些不同的样式。
```

CSS3的过度transition属性是一个复合属性，主要包括以下几个子属性：

- ```
  transition-property:指定过渡或动态模拟的CSS属性
  ```

- ```
  transition-duration:指定完成过渡所需的时间
  ```

- ```
  transition-timing-function:指定过渡函数
  ```

- ```
  transition-delay:指定开始出现的延迟时间
  ```

先来看**transition-property属性**

**transition-property**用来指定**过渡动画**的CSS属性名称，而这个过渡属性只有具备一个**中点值的属性**（需要产生动画的属性）才能具备过渡效果，其对应具有过渡的CSS属性主要有：

[![img](http://img.mukewang.com/5344eca300010a8005510421.jpg)](http://img.mukewang.com/5344eca300010a8005510421.jpg)

**HTML:**

```
<div></div>
```

**CSS:**

```
div {
  width: 200px;
  height: 200px;
  background-color:red;
  margin: 20px auto;
  -webkit-transition: background-color .5s ease .1s;
  transition: background-color .5s ease .1s;
}
div:hover {
  background-color: orange;
}
```

**演示结果:**

**鼠标移入**

**![img](http://img.mukewang.com/5344edf200019bde02130213.jpg)**

**鼠标移出**

**![img](http://img.mukewang.com/5344ee0500018c1b02110213.jpg)**

**特别注意**：当“transition-property”属性设置为**all**时，表示的是所有中点值的属性。

用一个简单的例子来说明这个问题：

假设你的初始状态设置了样式“width”,“height”,“background”,当你在终始状态都改变了这三个属性，那么**all**代表的就是“width”、“height”和“background”。如果你的终始状态只改变了“width”和“height”时，那么**all**代表的就是“width”和“height”。



## 过渡所需时间 transition-duration

**transition-duration**属性主要用来设置一个属性过渡到另一个属性所需的时间，也就是从旧属性过渡到新属性花费的时间长度，俗称**持续时间**。

**案例演示：**

在鼠标悬停（hover）状态下，让容器从直角慢慢过渡到圆角，并让整个动画持续0.5s。

HTML:

```
<div></div>
```

CSS:

```
div {
  width: 300px;
  height: 200px;
  background-color: orange;
  margin: 20px auto;
  -webkit-transition-property: -webkit-border-radius;
  transition-property: border-radius;
  -webkit-transition-duration: .5s;
  transition-duration: .5s;
  -webkit-transition-timing-function: ease-out;
  transition-timing-function: ease-out;
  -webkit-transition-delay: .2s;
  transition-delay: .2s;
}
div:hover {
  border-radius: 20px;
}
```

演示结果：

**鼠标移入**

![img](http://img.mukewang.com/5344efa00001144e03530225.jpg)

**鼠标移出**

![img](http://img.mukewang.com/5344efad0001949003320220.jpg)



## 过渡函数 transition-timing-function

transition-timing-function属性指的是过渡的“缓动函数”。主要用来指定浏览器的过渡速度，以及过渡期间的操作进展情况，其中要包括以下几种函数：

[![img](http://img.mukewang.com/5344f1320001481905640812.jpg)](http://img.mukewang.com/5344f1320001481905640812.jpg)

(单击图片可放大)

**案例展示：**

在hover状态下，让容器从一个正方形慢慢过渡到一个圆形，而整个过渡是先加速再减速，也就是运用ease-in-out函数。

**HTML代码:**

```
<div></div>
```

**CSS代码:**

```
div {
  width: 200px;
  height: 200px;
  background: red;
  margin: 20px auto;
  -webkit-transition-property: -webkit-border-radius;
  transition-property: border-radius;
  -webkit-transition-duration: .5s;
  transition-duration: .5s;
  -webkit-transition-timing-function: ease-in-out;
  transition-timing-function: ease-in-out;
  -webkit-transition-delay: .2s;
  transition-delay: .2s;
}
div:hover {
  border-radius: 100%;
}
```

演示结果

**鼠标移入：**

![img](http://img.mukewang.com/5344f1890001488f02360221.jpg)

**鼠标移出：**

![img](http://img.mukewang.com/5344f1920001d25102240230.jpg)

## 过渡延迟时间 transition-delay

**transition-delay属性**和**transition-duration属性**极其类似，不同的是transition-duration是用来设置过渡动画的持续时间，而transition-delay主要用来指定**一个动画开始执行的时间**，也就是说当改变元素属性值后多长时间开始执行。

有时我们想改变两个或者多个css属性的**transition效果**时，只要把几个transition的声明串在一起，用**逗号**（“，”）隔开，然后各自可以有各自不同的**延续时间**和其**时间的速率变换方式**。但需要值得注意的一点：第一个时间的值为 transition-duration，第二个为transition-delay。

例如：**a{ transition: background 0.8s ease-in 0.3,color 0.6s ease-out 0.3;}**

**示例演示：**

通过transition属性将一个200px *200px的橙色容器，在鼠标悬浮状态时，过渡到一个300px * 300px的红色容器。而且整个过渡0.1s后触发，并且整个过渡持续0.28s。

**HTML代码:**

```
<div class="wrapper">
  <div>鼠标放到我的身上来</div>
</div>
```

**CSS代码:**

```
.wrapper {
  width: 400px;
  height: 400px;
  margin: 20px auto;
  border: 2px dotted red;
}
.wrapper div {
  width: 200px;
  height: 200px;
  background-color: orange;
  -webkit-transition: all .28s ease-in .1s;
  transition: all .28s ease-in .1s;
}
.wrapper div:hover {
  width: 300px;
  height: 300px;
  background-color: red;
}
```

演示结果

**鼠标移入：**

![img](http://img.mukewang.com/5344f29e00012bbb04490423.jpg)

**鼠标移出：**

![img](http://img.mukewang.com/5344f2a70001dbfc04250421.jpg)

## 动画Keyframes介绍

`Keyframes`被称为**关键帧**，其类似于Flash中的关键帧。在CSS3中其主要以“@keyframes”开头，后面紧跟着是动画名称加上一对花括号“{…}”，括号中就是一些不同时间段样式规则。

```
@keyframes changecolor{
  0%{
   background: red;
  }
  100%{
    background: green;
  }
}
```

在一个“@keyframes”中的样式规则可以由多个百分比构成的，如在“0%”到“100%”之间创建更多个百分比，分别给每个百分比中给需要有动画效果的元素加上不同的样式，从而达到一种在不断变化的效果。

**经验与技巧：**在@keyframes中定义动画名称时，其中0%和100%还可以使用关键词**from**和**to**来代表，其中0%对应的是from，100%对应的是to。

浏览器的支持情况：

[![img](http://img.mukewang.com/534fa4450001513c05120121.jpg)](http://img.mukewang.com/534fa4450001513c05120121.jpg)**Chrome** 和 **Safari** 需要前缀 **-webkit-**；**Foxfire** 需要前缀 **-moz-**。

**案例演示**

通过“@keyframes”声明一个名叫“wobble”的动画，从“0%”开始到“100%”结束，同时还经历了一个“40%”和“60%”两个过程。“wobble”动画在“0%”时元素定位到left为100px，背景色为green，然后在“40%”时元素过渡到left为150px,背景色为orange,接着在“60%”时元素过渡到left为75px，背景色为blue，最后“100%”时结束动画，元素又回到起点left为100px处，背景色变为red。

HTML:

```
<div>鼠标放到我身上</div>
```

CSS:

```
@keyframes wobble {
  0% {
    margin-left: 100px;
    background:green;
  }
  40% {
    margin-left:150px;
    background:orange;
  }
  60% {
    margin-left: 75px;
    background: blue;
  }
  100% {
    margin-left: 100px;
    background: red;
  }
}
div {
  width: 100px;
  height: 100px;
  background:red;
  color: #fff;
}
div:hover{
  animation: wobble 5s ease .1s;
}
```



## CSS3中调用动画

**
animation-name属性**主要是用来调用 **@keyframes** 定义好的动画。需要特别注意: animation-name 调用的**动画名**需要和“@keyframes”**定义的动画名称**完全一致（**区分大小写**），如果不一致将不具有任何动画效果。

语法：

```
animation-name: none | IDENT[,none|DENT]*;
```

1、IDENT是由 **@keyframes** 创建的动画名，上面已经讲过了（animation-name 调用的动画名需要和“@keyframes”定义的动画名称完全一致）；

2、**none**为默认值，当值为 none 时，将没有任何动画效果,这可以用于覆盖任何动画。

注意：需要在 Chrome 和 Safari 上面的基础上加上-webkit-前缀，Firefox加上-moz-。



## CSS3中设置动画播放时间

animation-duration主要用来设置CSS3动画播放时间，其使用方法和transition-duration类似，是用来指定元素播放动画所持续的时间长，也就是**完成从0%到100%一次动画所需时间**。单位：S秒

**语法规则**

```
animation-duration: <time>[,<time>]*
```

取值<time>为数值，单位为秒，其默认值为“**0**”，这意味着动画周期为“0”，也就是没有动画效果（如果值为负值会被视为“0”）。

**案例演示：**

制作一个矩形变成圆形的动画，整个动画播放时间持续了10s钟。

HTML:

```
<div>Hover Me</div>
```

CSS:

```
@keyframes toradius{
  from {
    border-radius: 0;
  }
  to {
    border-radius: 100%;
  }
}
div {
  width: 200px;
  height: 200px;
  line-height: 200px;
  text-align: center;
  color: #fff;
  background: green;
  margin: 20px auto;
}
div:hover {
  animation-name: toradius;
  animation-duration: 10s;
  animation-timing-function: ease-in-out;
  animation-delay: .1s;
}
```

鼠标移入

![img](http://img.mukewang.com/534b8a930001f26e02260209.jpg)

鼠标移出

![img](http://img.mukewang.com/534b8a9b0001916b02660237.jpg)



## CSS3中设置动画播放方式

animation-timing-function属性主要用来设**置动画播放方式**。主要让元素根据时间的推进来改变属性值的变换速率，简单点说就是动画的播放方式。

**语法规则：**

```
animation-timing-function:ease | linear | ease-in | ease-out | ease-in-out | cubic-bezier(<number>, <number>, <number>, <number>) [, ease | linear | ease-in | ease-out | ease-in-out | cubic-bezier(<number>, <number>, <number>, <number>)]*
```

它和transition中的transition-timing-function一样，具有以下几种变换方式：ease,ease-in,ease-in-out,ease-out,linear和cubic-bezier。对应功如下：

```
![img](http://img.mukewang.com/534b8bb100016e9f05690795.jpg)
在调用move动画播放中，让元素样式从初始状态到终止状态时，先加速再减速，也就是渐显渐隐效果。
```



## CSS3中设置动画开始播放的时间

animation-delay属性用来定义动画开始播放的时间，用来触发动画播放的时间点。和transition-delay属性一样，用于定义在浏览器开始执行动画之前等待的时间。

**语法规则：**

```
animation-delay:<time>[,<time>]*
```

**案例演示：**   

浏览器渲染样式之后2S之后触发move动画。

**HTML:**

```
<div><span></span></div>
```

**CSS:**

```
@keyframes move {
  0%{
    transform: translate(0);
  }
  15%{
    transform: translate(100px,180px);
  }
  30%{
    transform: translate(150px,0);
  }
  45%{
    transform: translate(250px,180px);
  }
  60%{
    transform:translate(300px,0);
  }
  75%{
    transform: translate(450px,180px);
  }
  100%{
    transfrom: translate(480px,0);
  }
}
div {
  width: 500px;
  height: 200px;
  border: 1px solid red;
  margin: 20px auto;
}
div span {
  display: inline-block;
  width: 20px;
  height: 20px;
  background: green;
  border-radius: 100%;
  animation-name:move;
  animation-duration: 10s;
  animation-timing-function:ease;
  animation-delay:2s;
  animation-iteration-count:infinite;
}
```

结果展示：[![img](http://img.mukewang.com/5360bd2c00014b8505220221.jpg)](http://img.mukewang.com/5360bd2c00014b8505220221.jpg)



## CSS3中设置动画播放次数

animation-iteration-count属性主要用来定义动画的**播放次数。**

**语法规则：**

```
animation-iteration-count: infinite | <number> [, infinite | <number>]*
```

1、其值通常为**整数**，但也可以使用带有小数的数字，其默认值为1，这意味着动画将从开始到结束只播放一次。

2、如果取值为`**infinite**`，动画将会无限次的播放。

**举例：**

通过animation-iteration-count属性让动画move只播放5次，代码设置为：

```
animation-iteration-count:5;
```

**注意：Chrome或Safari浏览器，需要加入-webkit-前缀！**



## CSS3中设置动画播放方向

animation-direction属性主要用来设置**动画播放方向，**其语法规则如下：

```
animation-direction:normal | alternate [, normal | alternate]*
```

其主要有两个值：**normal**、**alternate**

1、**normal**是默认值，如果设置为normal时，动画的每次循环都是向前播放；

2、另一个值是**alternate**，他的作用是，动画播放在**第偶数次**向前播放，**第奇数次**向反方向播放。

例如：通过animation-direction属性，将move动画播放动画方向设置为alternate，代码为：

```
animation-direction:alternate;
```

**注意：Chrome或Safari浏览器，需要加入-webkit-前缀！**



## 设置动画的播放状态

animation-play-state属性主要用来控制元素动画的**播放状态**。

**参数：**

其主要有两个值：**running**和**paused**。

其中running是其默认值，主要作用就是类似于音乐播放器一样，可以通过paused将正在播放的动画停下来，也可以通过running将暂停的动画重新播放，这里的重新播放不一定是从元素动画的开始播放，而是从暂停的那个位置开始播放。另外如果暂停了动画的播放，元素的样式将回到最原始设置状态。

例如，页面加载时，动画不播放。代码如下：

```
animation-play-state:paused;
```



## CSS3中设置动画时间外属性

animation-fill-mode属性定义在动画开始之前和结束之后发生的操作。主要具有四个属性值：**none、forwards、backwords**和**both**。其四个属性值对应效果如下：

| **属性值** | **效果**                                                     |
| ---------- | ------------------------------------------------------------ |
| none       | 默认值，表示动画将按预期进行和结束，在动画完成其最后一帧时，动画会反转到初始帧处 |
| forwards   | 表示动画在结束后继续应用最后的关键帧的位置                   |
| backwards  | 会在向元素应用动画样式时迅速应用动画的初始帧                 |
| both       | 元素动画同时具有forwards和backwards效果                      |

在默认情况之下，动画不会影响它的关键帧之外的属性，使用animation-fill-mode属性可以修改动画的默认行为。简单的说就是告诉动画在第一关键帧上等待动画开始，或者在动画结束时停在最后一个关键帧上而不回到动画的第一帧上。或者同时具有这两个效果。

例如：让动画停在最一帧处。代码如下：

```
 animation-fill-mode:forwards; 
```



## 多列布局——Columns

为了能在Web页面中方便实现类似报纸、杂志那种多列排版的布局，W3C特意给CSS3增加了一个**多列布局模块**（CSS Multi Column Layout Module）。它主要应用在文本的**多列布局**方面，这种布局在报纸和杂志上都使用了几十年了，但要在Web页面上实现这样的效果还是有相当大的难度，庆幸的是，CSS3的多列布局可以轻松实现。接下来咱们一起学习多列布局相关的知识。

**语法：**

```
columns：<column-width> || <column-count>
```

多列布局columns属性参数主要就两个属性参数：列宽和列数。

| **参数**       | **参数说明**                 |
| -------------- | ---------------------------- |
| <column-width> | 主要用来定义多列中每列的宽度 |
| <column-count> | 主要用来定义多列中的列数     |

举例：要显示2栏显示，每栏宽度为200px，代码为：

```
columns: 200px 2;
```

到目前为止大部分主流浏览器都对其支持：

[![img](http://img.mukewang.com/5360c43c00010efd05080132.jpg)](http://img.mukewang.com/5360c43c00010efd05080132.jpg)



### 多列布局——column-width

column-width的使用和CSS中的width属性一样，不过不同的是，column-width属性在定义元素列宽的时候，既可以单独使用，也可以和多列属性中其他属性配合使用。其基本语法如下所示 ；

```
column-width: auto | <length>
```

取值说明

| **属性值** | **说明**                                                     |
| ---------- | ------------------------------------------------------------ |
| auto       | 如果column-width设置值为auto或者没有显式的设置值时，元素多列的列宽将由其他属性来决定，比如前面的示例就是由列数column-count来决定。 |
| <length>   | 使用固定值来设置元素列的宽度，其主要是由数值和长度单位组成，不过其值只能是正值，不能为负值。 |

```css
.columns {
  padding: 5px;
  border: 1px solid green;
  width: 900px;
  margin: 20px auto;
  
  -webkit-column-width:200px;
  -moz-column-width:200px;
  -o-column-width:200px;
  -ms-column-width:200px;
  column-width:200px;
  
  -webkit-column-count:3;
  -moz-column-count:3;
  -o-column-count:3;
  -ms-column-count:3;
  column-count:3;
}
```

### 多列布局——column-count

column-count属性主要用来给元素指定想要的列数和允许的最大列数。其语法规则：

```
column-count：auto | <integer>
```

**取值说明：**

| **属性值** | **属性值说明**                                               |
| ---------- | ------------------------------------------------------------ |
| auto       | 此值为column-count的默认值，表示元素只有一列，其主要依靠浏览器计算自动设置。 |
| <integer>  | 此值为正整数值，主要用来定义元素的列数，取值为大于0的整数，负值无效。 |

 例如：将列分成四列显示，代码如下：

```
column-count:4;
```

### 列间距column-gap

column-gap主要用来设置列与列之间的**间距**，其语法规则如下：

```
column-gap: normal || <length>
```

**取值说明**

| **属性值** | **属性值说明**                                               |
| ---------- | ------------------------------------------------------------ |
| normal     | 默认值，默值为1em（如果你的字号是px，其默认值为你的font-size值）。 |
| <length>   | 此值用来设置列与列之间的距离，其可以使用px,em单位的任何整数值，但不能是负值。 |

例如：将内容分三列显列，列与列之间的间距为2em，实现代码为：

```
column-count: 3;
column-gap: 2em;
```



### 列表边框column-rule

column-rule主要是用来定义列与列之间的**边框宽度、边框样式**和**边框颜色**。简单点说，就有点类似于常用的border属性。但column-rule是不占用任何空间位置的，在列与列之间改变其宽度不会改变任何列的位置。

**语法规则：**

```
column-rule:<column-rule-width>|<column-rule-style>|<column-rule-color>
```

**取值说明：**

| **属性值**        | **属性值说明**                                               |
| ----------------- | ------------------------------------------------------------ |
| column-rule-width | 类似于border-width属性，主要用来定义列边框的宽度，其默认值为“medium”，column-rule-width属性接受任意浮点数，但不接收负值。但也像border-width属性一样，可以使用关键词：medium、thick和thin。 |
| column-rule-style | 类似于border-style属性，主要用来定义列边框样式，其默认值为“none”。column-rule-style属性值与border-style属值相同，包括none、hidden、dotted、dashed、solid、double、groove、ridge、inset、outset。 |
| column-rule-color | 类似于border-color属性，主要用来定义列边框颜色，其默认值为前景色color的值，使用时相当于border-color。column-rule-color接受所有的颜色。如果不希望显示颜色，也可以将其设置为transparent(透明色) |

例如：为了能有效区分栏目列之间的关系，可以为其设置一个列边框，代码为：

```
column-rule: 2px dotted green;
```



### 跨列设置column-span

column-span主要用来定义一个分列元素中的子元素能跨列多少。column-width、column-count等属性能让一元素分成多列，不管里面元素如何排放顺序，他们都是从左向右的放置内容，但有时我们需要基中一段内容或一个标题不进行分列，也就是横跨所有列，此时column-span就可以轻松实现，此属性的语法如下。

```
column-span: none | all
```

**取值说明**

| **属性值** | **属性值说明**                                               |
| ---------- | ------------------------------------------------------------ |
| none       | 此值为column-span的默认值，表示不跨越任何列。                |
| all        | 这个值跟none值刚好相反，表示的是元素跨越所有列，并定位在列的Ｚ轴之上。 |

例如：将第一个标题跨越所有列，代码：

```
column-span:all;
```

效果如下：

[![img](http://img.mukewang.com/5365d594000190af09240316.jpg)](http://img.mukewang.com/5365d594000190af09240316.jpg)

