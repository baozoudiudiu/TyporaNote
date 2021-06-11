### 内联元素

```css
display: inline;
```

### 块级元素

```css
display: block;
```

### 内联块状元素

```css
display: inline-block;
```

### 流动布局（flow）：

先来说一说**流动模型**，流动（Flow）是默认的网页布局模式。也就是说网页在默认状态下的 HTML 网页元素都是根据流动模型来分布网页内容的。

流动布局模型具有2个比较典型的特征：

第一点，**块状元素**都会在所处的**包含元素内**自上而下按顺序垂直延伸分布，因为在默认状态下，块状元素的宽度都为**100%**。实际上，块状元素都会以行的形式占据位置。如右侧代码编辑器中三个块状元素标签(div，h1，p)宽度显示为100%。

在流动模型下，**内联元素**都会在所处的包含元素内从左到右水平分布显示。（内联元素可不像块状元素这么霸道独占一行）

右侧代码编辑器中内联元素标签a、span、em、strong都是内联元素。

### 浮动布局

```css
{
	float: left;
}
```

块状元素这么霸道都是独占一行，如果现在我们想让两个块状元素并排显示，怎么办呢？不要着急，设置元素浮动就可以实现这一愿望。

任何元素在默认情况下是不能浮动的，但可以用 CSS 定义为浮动，如 div、p、table、img 等元素都可以被定义为浮动。如下代码可以实现两个 div 元素一行显示。

```
div{
    width:200px;
    height:200px;
    border:2px red solid;
    float:left;
}
<div id="div1"></div>
<div id="div2"></div>
```

效果图

[![img](http://img.mukewang.com/540e62c60001c56a06760417.jpg)](http://img.mukewang.com/540e62c60001c56a06760417.jpg)

当然你也可以同时设置两个元素右浮动也可以实现一行显示。

```
div{
    width:200px;
    height:200px;
    border:2px red solid;
    float:right;
}
```

效果图

[![img](http://img.mukewang.com/540e632b0001f5f506760417.jpg)](http://img.mukewang.com/540e632b0001f5f506760417.jpg)

又有小伙伴问了，设置两个元素一左一右可以实现一行显示吗？当然可以：

```
div{
    width:200px;
    height:200px;
    border:2px red solid;
}
#div1{float:left;}
#div2{float:right;}
```

效果图

[![img](http://img.mukewang.com/540e63b50001f6a206760417.jpg)](http://img.mukewang.com/540e63b50001f6a206760417.jpg)



### 层模型有三种形式：

1、**绝对定位**(position: absolute)

2、**相对定位**(position: relative)

3、**固定定位**(position: fixed)

```css
{
	position: absolute | relative | fixed;
}
```

#### 绝对定位：

```css
div{
    width:200px;
    height:200px;
    border:2px red solid;
    position:absolute;
    left:100px;
    top:50px;
}
```

#### 相对定位：

如果想为元素设置层模型中的相对定位，需要设置position:relative（表示相对定位），它通过left、right、top、bottom属性确定元素在**正常文档流中**的偏移位置。相对定位完成的过程是首先按static(float)方式生成一个元素(并且元素像层一样浮动了起来)，然后相对于**以前的位置移动，**移动的方向和幅度由left、right、top、bottom属性确定，偏移前的位置保留不动。

如下代码实现相对于以前位置向下移动50px，向右移动100px;

```
#div1{
    width:200px;
    height:200px;
    border:2px red solid;
    position:relative;
    left:100px;
    top:50px;
}

<div id="div1"></div>
```


效果图：

![img](http://img.mukewang.com/53a00d2b00015c4b06190509.jpg)

什么叫做“偏移前的位置保留不动”呢？

大家可以做一个实验，在右侧代码编辑器的19行div标签的后面加入一个span标签，在标并在span标签中写入一些文字。如下代码：

```
<body>
    <div id="div1"></div><span>偏移前的位置还保留不动，覆盖不了前面的div没有偏移前的位置</span>
</body>
```

效果图：

[![img](http://img.mukewang.com/541a4bfc0001abef05940489.jpg)](http://img.mukewang.com/541a4bfc0001abef05940489.jpg)

从效果图中可以明显的看出，虽然div元素相对于以前的位置产生了偏移，但是div元素以前的位置还是保留着，所以后面的span元素是显示在了div元素以前位置的后面。

#### 固定定位

fixed：表示固定定位，与absolute定位类型类似，但它的相对移动的坐标是视图（屏幕内的网页窗口）本身。由于视图本身是固定的，它不会随浏览器窗口的滚动条滚动而变化，除非你在屏幕中移动浏览器窗口的屏幕位置，或改变浏览器窗口的显示大小，因此固定定位的元素会始终位于浏览器窗口内视图的某个位置，不会受文档流动影响，这与background-attachment:fixed;属性功能相同。以下代码可以实现相对于浏览器视图向右移动100px，向下移动50px。并且拖动滚动条时位置固定不变。

```css
#div1{
    width:200px;
    height:200px;
    border:2px red solid;
    position:fixed;
    left:100px;
    top:50px;
}
<p>文本文本文本文本文本文本文本文本文本文本文本文本文本文本文本文本文本文本文本文本文本文本文本文本文本文本文本文本文本文本文本文本文本文本。</p>
....
```

### 弹性盒模型 - 弹性盒模型之flex

详见`flex布局.md`文件。

### 水平或垂直居中

#### 行内元素

我们在实际工作中常会遇到需要设置水平居中的场景，比如为了美观，文章的标题一般都是水平居中显示的。

这里我们又得分两种情况：[行内元素](http://www.imooc.com/code/2049) 还是 [块状元素](http://www.imooc.com/code/2048) ，块状元素里面又分为定宽块状元素，以及不定宽块状元素。今天我们先来了解一下行内元素怎么进行水平居中？

如果被设置元素为文本、图片等行内元素时，水平居中是通过给**父元素**设置 `text-align:center` 来实现的。(父元素和子元素：如下面的html代码中，div是“我想要在父容器中水平居中显示”这个文本的父元素。反之这个文本是div的子元素 )如下代码：

html代码：

```html
<body>
  <div class="txtCenter">我想要在父容器中水平居中显示。</div>
</body>
```

css代码：

```html
<style>
  .txtCenter{
    text-align:center;
  }
</style>
```

#### 定宽块状元素

当被设置元素为 [块状元素](http://www.imooc.com/code/2048) 时用 text-align：center 就不起作用了，这时也分两种情况：**定宽**块状元素和**不定宽**块状元素。

这一小节我们先来讲一讲定宽块状元素。(定宽块状元素：块状元素的宽度width为固定值。)

满足定宽和块状两个条件的元素是可以通过设置“左右margin”值为“auto”来实现居中的。我们来看个例子就是设置 div 这个块状元素水平居中：

html代码：

```html
<body>
  <div>我是定宽块状元素，哈哈，我要水平居中显示。</div>
</body>
```

css代码：

```html
<style>
div{
    border:1px solid red;/*为了显示居中效果明显为 div 设置了边框*/
    
    width:200px;/*定宽*/
    margin:20px auto;/* margin-left 与 margin-right 设置为 auto */
}

</style>
```

也可以写成：

```css
margin-left:auto;
margin-right:auto;
```

这一章节我们来学习已知宽高实现盒子水平垂直居中。通常使用定位完成，例如想要实现以下效果：

[![img](https://img4.mukewang.com/5e967bb40001e35725570475.jpg)](https://img4.mukewang.com/5e967bb40001e35725570475.jpg)

我们有如下两个div元素

![img](https://img3.mukewang.com/5e967a0500013c9104650162.jpg)

要实现子元素相对于父元素垂直水平居中,我们只需要输入以下代码：

[![img](https://img.mukewang.com/5e967a380001840f11050487.jpg)](https://img.mukewang.com/5e967a380001840f11050487.jpg)

**技术点的解释：**

1、利用父元素设置相对定位,子元素设置绝对定位,那么子元素就是相对于父元素定位的特性。

2、子元素设置上和左偏移的值都为50%，是元素的左上角在父元素中心点的位置。效果：

[![img](https://img2.mukewang.com/5e967c3d0001fbbf25600616.jpg)](https://img2.mukewang.com/5e967c3d0001fbbf25600616.jpg)

3、然后再用margin给上和左都给负的自身宽高的一半,就能达到垂直水平居中的效果。

#### 不定宽高



未知宽高实现盒子水平垂直居中，通常使用定位以及translate完成。参考下面例子：

```
 <div class="box">
        <div class="box1">
            慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网慕课网
        </div>
    </div>
```

添加样式：

```
 .box {
        border: 1px solid #00ee00;
        height: 300px;
        position: relative;

    }

    .box1 {
        border: 1px solid red;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }
```

效果如下：

[![img](https://img4.mukewang.com/5e967f3b000117da25530461.jpg)](https://img4.mukewang.com/5e967f3b000117da25530461.jpg)