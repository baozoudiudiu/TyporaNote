## 盒子模型

1. **W3C标准盒模型**

```
外盒尺寸计算（元素空间尺寸）

element空间高度＝内容高度＋内距＋边框＋外距

element空间宽度＝内容宽度＋内距＋边框＋外距

内盒尺寸计算（元素大小）

element高度＝内容高度＋内距＋边框（height为内容高度）

element宽度＝内容宽度＋内距＋边框（width为内容宽度）
```

**2.IE传统下盒模型（IE6以下，不包含IE6版本或”QuirksMode下IE5.5+”）**

```
外盒尺寸计算（元素空间尺寸）

element空间高度＝内容高度＋外距（height包含了元素内容宽度、边框、内距）

element宽间宽度＝内容宽度＋外距（width包含了元素内容宽度、边框、内距）

内盒尺寸计算（元素大小）

element高度＝内容高度（height包含了元素内容宽度、边框、内距）

element宽度＝内容宽度（width包含了元素内容宽度、边框、内距）
```



在CSS3中新增加了**box-sizing**属性，能够事先定义盒模型的尺寸解析方式，其语法规则如下：

```
box-sizing: content-box | border-box | inherit
```

**取值说明**

| **属性值**  | **属性值说明**                                               |
| ----------- | ------------------------------------------------------------ |
| content-box | 默认值，其让元素维持W3C的标准盒模型，也就是说元素的宽度和高度（width/height）等于元素边框宽度（border）加上元素内距（padding）加上元素内容宽度或高度（content width/ height），也就是element width/height = border + padding + content width / height |
| border-box  | 重新定义CSS2.1中盒模型组成的模式，让元素维持IE传统的盒模型（IE6以下版本和IE6-7怪异模式），也就是说元素的宽度或高度等于元素内容的宽度或高度。从上面盒模型介绍可知，这里的内容宽度或高度包含了元素的border、padding、内容的宽度或高度（此处的内容宽度或高度＝盒子的宽度或高度—边框—内距）。 |
| inherit     | 使元素继承父元素的盒模型模式                                 |

其中最为关键的是box-sizing中content-box和border-box两者的区别，他们之间的区别可以通过下图来展示，其对盒模型的不同解析：

[![img](http://img.mukewang.com/5365d98000018fa606460416.jpg)](http://img.mukewang.com/5365d98000018fa606460416.jpg)



## 伸缩布局

CSS3引入了一种新的布局模式——**Flexbox布局**，即**伸缩布局盒模型**（Flexible Box），用来提供一个更加有效的方式制定、调整和分布一个容器里项目布局，即使它们的大小是未知或者动态的，这里简称为**Flex**。

Flexbox布局常用于设计比较复杂的页面，可以轻松的实现屏幕和浏览器窗口大小发生变化时保持元素的相对位置和大小不变，同时减少了依赖于浮动布局实现元素位置的定义以及重置元素的大小。

Flexbox布局在定义伸缩项目大小时伸缩容器会预留一些可用空间，让你可以调节伸缩项目的相对大小和位置。例如，你可以确保伸缩容器中的多余空间平均分配多个伸缩项目，当然，如果你的伸缩容器没有足够大的空间放置伸缩项目时，浏览器会根据一定的比例减少伸缩项目的大小，使其不溢出伸缩容器。综合而言，Flexbox布局功能主要具有以下几点：

第一，屏幕和浏览器窗口大小发生改变也可以灵活调整布局；

第二，可以指定伸缩项目沿着主轴或侧轴按比例分配额外空间（伸缩容器额外空间），从而调整伸缩项目的大小；

第三，可以指定伸缩项目沿着主轴或侧轴将伸缩容器额外空间，分配到伸缩项目之前、之后或之间；

第四，可以指定如何将垂直于元素布局轴的额外空间分布到该元素的周围；

第五，可以控制元素在页面上的布局方向；

第六，可以按照不同于文档对象模型（DOM）所指定排序方式对屏幕上的元素重新排序。也就是说可以在浏览器渲染中不按照文档流先后顺序重排伸缩项目顺序。

Flexbox规范版本众多，浏览器对此语法支持度也各有不同，接下来的内容以最新语法版本为例向大家展示：

**1.创建一个flex容器**

任何一个flexbox布局的第一步是需要创建一个flex容器。为此给元素设置display属性的值为flex。在Safari浏览器中，你依然需要添加前缀-webkit，

```
.flexcontainer{ display: -webkit-flex; display: flex; }
```

**2.Flex项目显示**

Flex项目是Flex容器的子元素。他们沿着主要轴和横轴定位。默认的是沿着水平轴排列一行。你可以通过flex-direction来改变主轴方向修改为column，其默认值是row。

[![img](http://img.mukewang.com/5365e24300018b8005570159.jpg)](http://img.mukewang.com/5365e24300018b8005570159.jpg)

**3.Flex项目列显示**

```
.flexcontainer{ display: -webkit-flex; display: flex; -webkit-flex-direction: column; flex-direction: column; }
![img](http://img.mukewang.com/5365e2b300016b2405570509.jpg)
```

**4.Flex项目移动到顶部**

如何实现将flex项目移动到顶部的效果，关键点：取决于主轴的方向。**justify-content** 属性定义了项目在主轴上的对齐方式。**align-items** 属性定义项目在交叉轴上如何对齐。 如果主轴是水平的方向，通过**align-items**设置；如果主轴是垂直的方向，通过**justify-content**设置。

```
.flexcontainer{ -webkit-flex-direction: column; flex-direction: column; -webkit-justify-content: flex-start; justify-content: flex-start; }
```

[![img](http://img.mukewang.com/5365e694000180fd05570538.jpg)](http://img.mukewang.com/5365e694000180fd05570538.jpg)

```
.flexcontainer{ display: -webkit-flex; display: flex; -webkit-flex-direction: row; flex-direction: row; -webkit-align-items: flex-start; align-items: flex-start; }
```

[![img](http://img.mukewang.com/5365e7160001b9e405570203.jpg)](http://img.mukewang.com/5365e7160001b9e405570203.jpg)



Flexbox规范版本众多，浏览器对此语法支持度也各有不同，接下来的内容以最新语法版本为例向大家展示：**（接上一节）**

**5.Flex项目移到左边**

flex项目称动到左边或右边也取决于主轴的方向。如果flex-direction设置为row，设置justify-content控制方向；如果设置为column，设置align-items控制方向。

```
.flexcontainer{ display: -webkit-flex; display: flex; -webkit-flex-direction: row; flex-direction: row; -webkit-justify-content: flex-start; justify-content: flex-start; }
```

[![img](http://img.mukewang.com/5365e8f700012f8a05570207.jpg)](http://img.mukewang.com/5365e8f700012f8a05570207.jpg)

```
.flexcontainer{ display: -webkit-flex; display: flex; -webkit-flex-direction: column; flex-direction: column; -webkit-align-items: flex-start; align-items: flex-start; }
```

[![img](http://img.mukewang.com/5365e9e00001fd9305570449.jpg)](http://img.mukewang.com/5365e9e00001fd9305570449.jpg)

**6.Flex项目移动右边**

`.flexcontainer{ display: -webkit-flex; display: flex; -webkit-flex-direction: row; flex-direction: row; -webkit-justify-content: flex-end; justify-content: flex-end; }`[![img](http://img.mukewang.com/5365ea440001835305570196.jpg)](http://img.mukewang.com/5365ea440001835305570196.jpg)

```
.flexcontainer{ display: -webkit-flex; display: flex; -webkit-flex-direction: column; flex-direction: column; -webkit-align-items: flex-end; align-items: flex-end; }
```

[![img](http://img.mukewang.com/5365ebe9000199b107620445.jpg)](http://img.mukewang.com/5365ebe9000199b107620445.jpg)

**7.水平垂直居中**

在Flexbox容器中制作水平垂直居中是微不足道的。设置justify-content或者align-items为**center**。另外根据主轴的方向设置flex-direction为row或column。

```
.flexcontainer{ display: -webkit-flex; display: flex; -webkit-flex-direction: row; flex-direction: row; -webkit-align-items: center; align-items: center; -webkit-justify-content: center; justify-content: center; }
```

[![img](http://img.mukewang.com/5365ec680001868c07620314.jpg)](http://img.mukewang.com/5365ec680001868c07620314.jpg)

```
.flexcontainer{ display: -webkit-flex; display: flex; -webkit-flex-direction: column; flex-direction: column; -webkit-align-items: center; align-items: center; -webkit-justify-content: center; justify-content: center; }
```

[![img](http://img.mukewang.com/5365ecee00016b0107630450.jpg)](http://img.mukewang.com/5365ecee00016b0107630450.jpg)

**8.Flex项目实现自动伸缩**

您可以定义一个flex项目，如何相对于flex容器实现自动的伸缩。需要给每个flex项目设置flex属性设置需要伸缩的值。

```
.bigitem{ -webkit-flex:200; flex:200; }  .smallitem{ -webkit-flex:100; flex:100; }
```

[![img](http://img.mukewang.com/5365ed860001a8a907620321.jpg)](http://img.mukewang.com/5365ed860001a8a907620321.jpg)



## meta标签

最后还有一个不可或缺的东东，那就是meta标签，可以说，在响应式设计中如果没有这个meta标签，你就是蹩脚的，响应式设计就是空谈。

个meta标签被称为可视区域meta标签，其使用方法如下。

```
<meta name=”viewport” content=”” />
```

在content属性中主要包括以下属性值，用来处理可视区域。

[![img](http://img.mukewang.com/53660f2c0001190005270386.jpg)](http://img.mukewang.com/53660f2c0001190005270386.jpg)

在实际项目中，为了让Responsive设计在智能设备中能显示正常，也就是浏览Web页面适应屏幕的大小，显示在屏幕上，可以通过这个可视区域的**meta标签**进行重置，告诉他使用设备的宽度为视图的宽度，也就是说禁止其默认的自适应页面的效果，具体设置如下：

```
<meta name=”viewport” content=”width=device-width,initial-scale=1.0” />
```

另外一点，由于Responsive设计是结合CSS3的Media Queries属性，才能尽显Responsive设计风格，但大家都清楚，**在IE6-8中完全是不支持CSS3 Media**。下面我们一起来看看CSS3 Meida Queries在标准设备上的运用，大家可以把这些样式加到你的样式文件中，或者单独创建一个名为“responsive.css”文件，并在相应的条件中写上你的样式，让他适合你的设计需求。

脚本下载地址： 

```
media-queries.js(http://code.google.com/p/css3-mediaqueries-js/)      

 respond.js(https://github.com/scottjehl/Respond)

 <!—[if lt IE9]>
      <scriptsrc=http://css3-mediaqueries-js.googlecode.com/svn/trunk/css3-mediaqueries.js></script>
 <![endif]>
```



## 自由缩放属性resize

为了增强用户体验，CSS3增加了很多新的属性，其中**resize**就是一个重要的属性，它允许用户通过拖动的方式来修改元素的尺寸来改变元素的大小。到目前为止，可以使用overflow属性的任何容器元素。

在此之前，Web设计师为了要实现这样具有拖动效果的UI，使用大量的脚本代码才能实现，这样费时费力，效率极低。

resize属性主要是用来改变元素尺寸大小的，其主要目的是增强用户体验。但使用方法却是极其的简单，先从其语法入手。

```
resize: none | both | horizontal | vertical | inherit
```

**取值说明：**

| **属性值** | **取值说明**                                                 |
| ---------- | ------------------------------------------------------------ |
| none       | 用户不能拖动元素修改尺寸大小。                               |
| both       | 用户可以拖动元素，同时修改元素的宽度和高度                   |
| horizontal | 用户可以拖动元素，仅可以修改元素的宽度，但不能修改元素的高度。 |
| vertical   | 用户可以拖动元素，仅可以修改元素的高度，但不能修改元素的宽度。 |
| inherit    | 继承父元素的resize属性值。                                   |

例如：通过resize属性，让文本域可以沿水平方向拖大。代码为：

```
textarea {
  -webkit-resize: horizontal;
  -moz-resize: horizontal;
  -o-resize: horizontal;
  -ms-resize: horizontal;
  resize: horizontal;
}
```



## CSS3外轮廓属性

外轮廓outline在页面中呈现的效果和边框border呈现的效果极其相似，但和元素边框border完全不同，外轮廓线不占用网页布局空间，不一定是矩形，外轮廓是属于一种动态样式，只有元素获取到焦点或者被激活时呈现。

outline属性早在CSS2中就出现了，主要是用来在元素周围绘制一条轮廓线，可以起到突出元素的作用。但是并未得到各主流浏览器的广泛支持，在CSS3中对outline作了一定的扩展，在以前的基础上增加新特性。outline属性的基本语法如下：

```
outline: ［outline-color］ || [outline-style] || [outline-width] || [outline-offset] || inherit
```

从语法中可以看出outline和border边框属性的使用方法极其类似。outline-color相当于border-color、outline-style相当于border-style，而outline-width相当于border-width，只不过CSS3给outline属性增加了一个`outline-offset`属性，其取值说明如下。

 

| **属性值**     | **属性值说明**                                               |
| -------------- | ------------------------------------------------------------ |
| outline-color  | 定义轮廓线的颜色，属性值为CSS中定义的颜色值。在实际应用中，可以将此参数省略，省略时此参数的默认值为黑色。 |
| outline-style  | 定义轮廓线的样式，属性为CSS中定义线的样式。在实际应用中，可以将此参数省略，省略时此参数的默认值为none，省略后不对该轮廓线进行任何绘制。 |
| outline-width  | 定义轮廓线的宽度，属性值可以为一个宽度值。在实际应用中，可以将此参数省略，省略时此参数的默认值为medium，表示绘制中等宽度的轮廓线。 |
| outline-offset | 定义轮廓边框的偏移位置的数值，此值可以取负数值。当此参数的值为正数值，表示轮廓边框向外偏离多少个像素；当此参数的值为负数值，表示轮廓边框向内偏移多少个像素。 |
| inherit        | 元素继承父元素的outline效果。                                |



## CSS生成内容

在Web中插入内容，在CSS2.1时代依靠的是JavaScript来实现。但进入CSS3进代之后我们可以通过CSS3的伪类“:before”，“:after”和CSS3的伪元素“::before”、“::after”来实现，其关键是依靠CSS3中的“content”属性来实现。不过这个属性对于**img**和**input**元素不起作用。

content配合CSS的伪类或者伪元素，一般可以做以下四件事情：

| **功能** | **功能说明**                                                 |
| -------- | ------------------------------------------------------------ |
| none     | 不生成任何内容                                               |
| attr     | 插入标签属性值                                               |
| url      | 使用指定的绝对或相对地址插入一个外部资源（图像，声频，视频或浏览器支持的其他任何资源） |
| string   | 插入字符串                                                   |

**实例展示：**

在CSS中有一种清除浮动的方法叫“clearfix”。而这个“clearfix”方法就中就使用了“content”，只不过只是在这里插入了一个空格。如下所示：

```
.clearfix:before,

.clearfix:after {

       content:””;

       display:table;

}

.clearfix:after {

       clear:both;

       overflow:hidden;

}
```

上面这个示例是最常见的，也是最简单的，我们再来看一个插入元素属性值的方法。

假设我们有一个元素：

<a href="##" title="我是一个title属性值，我插在你的后面">我是元素</a>

可以通过”:after”和”content:attr(title)”将元素的”title”值插入到元素内容“我是元素”之后：

```
a:after {

  content:attr(title);

       color:#f00;

}
```

效果如下：

 [![img](http://img.mukewang.com/5365fae20001649403560028.jpg)](http://img.mukewang.com/5365fae20001649403560028.jpg)