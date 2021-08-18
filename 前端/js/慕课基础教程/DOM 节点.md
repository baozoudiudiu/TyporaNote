# 获取和操作 DOM 节点

> DOM 节点也会被称为 DOM 元素。

想要操作 DOM 节点，就必须先获取到 DOM 节点。



## 1. 获取 DOM 节点

获取 DOM 节点的方式有很多，这里例举几个常用的，所有的 DOM 元素都具有以下方法：

- element.getElementById
- element.getElementByName
- element.getElementsByTagName
- element.getElementsByClassName
- element.querySelector
- element.querySelectorAll



### 1.1 element.getElementById

> 返回对拥有指定 id 的第一个对象的引用。

`element.getElementById` 是指去 `element` 节点下根据 id 查找子节点。

通常在程序开始前，没有主动去获取过节点，这个时候会使用根节点 `document` 来进行查找。

实例演示

```html
<div id="html-element">
  我是一个元素
</div>

<script>
  var element = document.getElementById('html-element');

  element.innerHTML = '<a href="//imooc.com">我变成了超链接</a>';
</script>
123456789
```

[运行案例](http://www.imooc.com/wiki/run/307.html)点击 "运行案例" 可查看在线运行效果

在使用 JavaScript 操作 DOM 节点的时候，也会把 DOM 节点称为 `DOM 对象`，以契合编程中`对象`的概念，更好理解。

以上例子通过 `document.getElementById` 获取 id 为 `html-element` 的 DOM 节点，并通过修改 `innerHTML` 属性，将这个节点的内容进行了修改。



### 1.2 element.getElementByName

> 返回带有指定名称的对象集合。

`element.getElementByName` 是通过元素的 `name` 属性进行查找的，过去操作表单的时候会经常用到。

实例演示

```html
<form>
  <div>
    <label>
      <input type="checkbox" name="skill" checked="checked" value="JavaScript"> JavaScript
    </label>

    <label>
      <input type="checkbox" name="skill" value="c++"> C++
    </label>

    <label>
      <input type="checkbox" name="skill" checked="checked" value="Java"> Java
    </label>
  </div>
</form>
<div id="result"></div>

<script>
  var checkboxes = document.getElementsByName('skill');

  var skills = [];

  checkboxes.forEach(function(checkbox) {
    if (checkbox.getAttribute('checked')) {
      skills.push(checkbox.value);
    }
  });

document.getElementById('result').innerHTML = '选中的技能：' + skills.join('、');
</script>
123456789101112131415161718192021222324252627282930
```

[运行案例](http://www.imooc.com/wiki/run/308.html)点击 "运行案例" 可查看在线运行效果

通过 `getElementsByName` 获取到的是 DOM 节点的集合，需要注意的是，这个集合不是数组类型的，而是 `NodeList` ，其不具备数组的 `map` 、`filter` 等方法，但是具备 `forEach` 方法。

> Tips：IE 和早期浏览器的 NodeList 是没有 forEach 方法的，具体版本可以通过 [Can I Use](https://caniuse.com/#feat=mdn-api_nodelist_foreach) 查看。



### 1.3 element.getElementsByTagName

> 返回带有指定标签名的对象集合。

`element.getElementsByTagName` 是通过标签名获取 DOM 节点的，返回的也是一个集合。

实例演示

```html
<div>
  <p>我是第一个段落。</p>
  <p>我是第二个段落。</p>
  <p>我是第三个段落。</p>
  <p>我是第四个段落。</p>
  <p>我是第五个段落。</p>
</div>
<div id="result" style="color: #4caf50;"></div>
<script>
  var pList = document.getElementsByTagName('p');

  var res = [];
  var i, len;
  for (i = 0, len = pList.length; i < len; i++) {
	res.push(pList[i].innerText);
  }
  
  document.getElementById('result').innerHTML = '所有 p 标签的内容：<br>' + res.join('<br>');
</script>
12345678910111213141516171819
```

[运行案例](http://www.imooc.com/wiki/run/309.html)点击 "运行案例" 可查看在线运行效果

此方法返回值的类型是 `HTMLCollection` ，不是 `NodeList` ，没有 `forEach` 方法。

可以使用 for 循环对返回值进行遍历。

> Tips： 特别要注意，此方法为 getElement`s`ByTagName，前往不要忘记有个 `s`。



### 1.4 element.getElementsByClassName

> 返回一个包含了所有指定类名的子元素的类数组对象。

`element.getElementsByClassName` 通过元素的类名来获取 DOM 节点。

实例演示

```html
<div>
  <div class="odd">1</div>
  <div class="even">2</div>
  <div class="odd">3</div>
  <div class="even">4</div>
  <div class="odd">5</div>
  <div class="even">6</div>
</div>
<div id="result"></div>
<script>
  var odd = document.getElementsByClassName('odd');

  var res = [];
 
  var i, len;
  for (i = 0, len = odd.length; i < len; i++) {
    res.push(odd[i].innerText);
  }

  var resultElement = document.getElementById('result');

  resultElement.innerHTML = '所有奇数：<br>' + res.join('<br>');
</script>
1234567891011121314151617181920212223
```

[运行案例](http://www.imooc.com/wiki/run/310.html)点击 "运行案例" 可查看在线运行效果

与 `getElementsByTagName` 返回值类型相同，此方法返回类型也是 `HTMLCollection`。

> Tips：注意，getElement`s`ByTagName 中也有 `s` 。同时此方法也不支持 IE8。



### 1.5 element.querySelector

> 文档对象模型 Document 引用的 querySelector () 方法返回文档中与指定选择器或选择器组匹配的第一个 html 元素 Element 。 如果找不到匹配项，则返回 null 。

`element.querySelector` 是获取 DOM 节点最常用的方法之一，可以传入 CSS 选择器来匹配获取 DOM 节点。

如使用 CSS 在给 id 为 `tip` 的元素设置红色字体样式的时候，选择器使用的是 `#tip`。

```css
#tip {
  color: red;
}


代码块123
```

使用 `element.querySelector` 获取 id 为 `tip` 的元素，传入的参数也是 `#tip`，与 CSS 选择器一致。

实例演示

```html
<div>
  <div id="tip">今日大甩卖！！一双袜子 <strong>三</strong> 块！三双袜子只要 <strong>十</strong> 块！！</div>
</div>

<script>
  var tip = document.querySelector('#tip');

  tip.style.color = 'red';
</script>
123456789
```

[运行案例](http://www.imooc.com/wiki/run/311.html)点击 "运行案例" 可查看在线运行效果

通过设置 `style` 下的 `color` 属性，可以更改字体颜色。通过 `style` 设置的样式都是内联样式。

即便传入的选择器能匹配到多个 DOM 对象，此方法也只会返回一个 DOM 对象。



### 1.6 element.querySelectorAll

> 返回与指定的选择器组匹配的文档中的元素列表 (使用深度优先的先序遍历文档的节点)。返回的对象是 NodeList 。

此方法传入的参数与 `querySelector` 一致，但会返回匹配到的所有 DOM 对象。

实例演示

```html
<ul>
  <li>我是列表1</li>
  <li>我是列表2</li>
  <li>我是列表3</li>
  <li>我是列表4</li>
</ul>

<button class="change">变！</button>

<script>
  var lis = document.querySelectorAll('li');
  var btn = document.querySelector('.change');

  btn.addEventListener('click', function() {
    lis.forEach(function(li, index) {
      li.innerText = index;
    });
  });
</script>
12345678910111213141516171819
```

[运行案例](http://www.imooc.com/wiki/run/312.html)点击 "运行案例" 可查看在线运行效果

`element.querySelectorAll` 返回的也是一个 `NodeList`。



## 2. 操作 DOM 节点

到目前为止已经做了许多 DOM 操作了，如使用 `innerText` 修改文本，使用 `style` 修改样式，这些其实都是在操作 DOM。

这里列举两个常用的操作。



### 2.1 修改 class 属性

修改节点的 class 属性，这个操作频率是非常高的。

如使用 class 来控制元素的显示与隐藏。

实例演示

```html
<style>
  .show {
    display: block;
  }

  .hidden {
    display: none;
  }
</style>

<p class="tip show">我要早睡早起，不能再熬夜了。</p>
<button class="toggle">切换</button>

<script>
  var toggleBtn = document.querySelector('.toggle');
  var tipEle = document.querySelector('.tip');

  toggleBtn.addEventListener('click', function() {
    var className = tipEle.className;

    if (className.indexOf('show') > -1) {
      tipEle.className = 'tip hidden';
      return;
    }

    tipEle.className = 'tip show';
  });
</script>
12345678910111213141516171819202122232425262728
```

[运行案例](http://www.imooc.com/wiki/run/313.html)点击 "运行案例" 可查看在线运行效果

通过 DOM 节点的 `className` 属性，来控制 class。

![图片描述](http://img.mukewang.com/wiki/5e82e2000a62c78711480432.jpg)



### 2.2 设置 / 获取其他属性

> 修改 class 也属于这个场景，但使用 className 更为频繁，所以单独拿出来介绍。

节点的许多状态是使用属性表示的，如`复选框`是否选中，就是由 `checked` 属性决定。

实例演示

```html
<label>
  <input type="checkbox" class="checkbox">
  爱我别走
</label>

<div style="margin-top: 16px;">
  <button class="toggle">切换!</button>
</div>

<script>
  var checkbox = document.querySelector('.checkbox');
  var toggleBtn = document.querySelector('.toggle');

  toggleBtn.onclick = function() {
    var checked = checkbox.getAttribute('checked');

    if (checked) {
      checkbox.removeAttribute('checked', '');
    } else {
      checkbox.setAttribute('checked', 'checked');
    }
  };
</script>
1234567891011121314151617181920212223
```

[运行案例](http://www.imooc.com/wiki/run/314.html)点击 "运行案例" 可查看在线运行效果

![图片描述](http://img.mukewang.com/wiki/5e82e2100a06da2209720432.jpg)

`getAttribute` 方法就可以获得某个属性的值。

`setAttribute` 用于给属性设置属性值。

`removeAttribute` 则是将属性从元素上移除。

这三个方法可以用于元素的任意属性，包括 `class` 。



## 3. 其他



### 3.1 将集合转化为数组

通过几种获取 DOM 节点的方法的返回值可以发现，当要获取多个 DOM 节点组成的集合的时候，返回的都不是数组。

```html
<div>
  <ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
  </ul>
</div>

<script>
  var lis = document.querySelectorAll('li');
  
  var filtered = lis.filter(function(li) {
    return Number(li.innerText % 2);
  });
</script>


代码块123456789101112131415
```

如使用上述例子对获取到的所有 DOM 节点 用 `filter` 方法进行过滤是会报错的。

这个时候就需要通过一些方式，来获得由 DOM 节点组成的数组。

#### 3.1.1 使用数组的 slice 方法

这里并不是让 DOM 节点的集合去调用 `slice` 方法，而是利用 `slice` 方法来将 DOM 节点的集合转化为数组。

实例演示

```html
<div>
  <ul>
    <li>i</li>
    <li>love</li>
    <li>imooc</li>
  </ul>
</div>

<script>
  var lisColl = document.querySelectorAll('li');
  
  var lisArray1 = [].slice.call(lisColl);
  var lisArray2 = Array.prototype.slice.call(lisColl);
  
	var map = function(li) {
    return li.innerText;
  };
  
  console.log(lisArray1.map(map).join(' ')); // 输出：i love imooc
  console.log(lisArray2.map(map).join(' ')); // 输出：i love imooc
</script>
123456789101112131415161718192021
```

[运行案例](http://www.imooc.com/wiki/run/316.html)点击 "运行案例" 可查看在线运行效果

`slice` 方法可以接收两个参数，分别是起始下标和结束下标，其作用是浅复制起始下标到结束下标的所有项，然后产生一个新数组返回，如果不提供参数，则直接浅复制所有项，形成一个新数组返回。

使用 `[].slice.call(类数组)` 或 `Array.prototype.slice.call(类数组)` 即可将一个类数组转化为数组。

通过在控制台观察 `NodeList` 和 `HTMLCollection` 类型，可以发现他们是符合类数组特性的。

![图片描述](http://img.mukewang.com/wiki/5e82e03109c80c4113400552.jpg)

所以就可以通过这种方式来转化成数组。

数组的 `slice` 方法在执行的时候内部是使用循环来操作数组项的，所以操作一个类数组不会出现问题，使用 `call` 方法将操作的数组指定为传入的伪数组，就达到了将类数组转化为数组的目的。

#### 3.1.2 将数组的原型方法挂载到目标对象的原型上

实例演示

```html
<div>
  <ul>
    <li>i</li>
    <li>love</li>
    <li>imooc</li>
  </ul>
</div>

<script>
  NodeList.prototype.join = Array.prototype.join; // 提供 join 方法

  var lisColl = document.querySelectorAll('li');

  lisColl.__proto__.map = Array.prototype.map; // 提供 map 方法

  var map = function(li) {
    return li.innerText;
  };

  console.log(lisColl.map(map).join(' ')); // 输出：i love imooc
</script>
123456789101112131415161718192021
```

[运行案例](http://www.imooc.com/wiki/run/317.html)点击 "运行案例" 可查看在线运行效果

通过在 `NodeList` 原型上提供数组的方法，就可以直接进行方法的调用。

其原理可以参考原型相关章节。

#### 3.1.3 使用 for 循环

使用 for 循环遍历集合，将每一项放入新数组。

实例演示

```html
<div>
  <ul>
    <li>i</li>
    <li>love</li>
    <li>imooc</li>
  </ul>
</div>

<script>
  var lisColl = document.querySelectorAll('li');
  var lis = [];
  
  var i, len;
  for (i = 0, len = lisColl.length; i < len; i++) {
    lis.push(lisColl[i]);
  }
  
  var str = lis
    .map(function(li) {
      return li.innerText
    })
    .join(' ');

  console.log(str); // 输出：i love imooc
</script>
12345678910111213141516171819202122232425
```

[运行案例](http://www.imooc.com/wiki/run/318.html)点击 "运行案例" 可查看在线运行效果

这种方式没有特殊情况通常不会去使用。

#### 3.1.4 使用 Array.from 方法

> `Array.from()` 方法从一个类似数组或可迭代对象创建一个新的，浅拷贝的数组实。(MDN)

`Array.from` 可以将一个类数组转化为数组。

```js
var arrayLike = {
  0: '9',
  1: '9',
  2: '6',
  3: ' bye!',
  length: 4,
};

var str = Array.from(arrayLike).join('');

console.log(str); // 输出：996 bye!


代码块1234567891011
```

**该方法由 `ES2015` 提供，所以旧版的浏览器不支持。**

#### 3.1.5 使用扩展运算符

扩展运算符也是由 `ES2015` 提供的。

实例演示

```html
<div>
  <ul>
    <li>i</li>
    <li>love</li>
    <li>imooc</li>
  </ul>
</div>

<script>
  var lisColl = document.querySelectorAll('li');
  var arr = [...lisColl];
  
  console.log(Array.isArray(lisColl)); // 输出：false
  console.log(Array.isArray(arr)); // 输出：true
</script>
123456789101112131415
```

[运行案例](http://www.imooc.com/wiki/run/320.html)点击 "运行案例" 可查看在线运行效果

`...` 即扩展运算符，根据使用场景，他还能被作为剩余参数操作符使用。

通过 `Array.isArray` 可以判断一个值是不是数组。



### 3.2 null 判断

当获取节点的方法没有匹配到任何元素的时候，是可能返回 null 或者 空集合的。

```js
var el = document.querySelector('#dfsafds');
var elList = document.querySelectorAll('.dfsafds');

el.innerHTML = '<p>我写的代码从来不会报错！</p>';
elList[1].innerHTML = '<p>我写的代码从来不会报错！</p>';

// Cannot set property 'innerHTML' of null


代码块1234567
```

碰到这种情况，上述代码就报错了，假如后面代码存在渲染逻辑，则不会再继续执行，最后换来一份 `辞退报告`。

所以在没有把握的情况下一定要进行空判断。

```js
var el = document.querySelector('#dfsafds');

if (el) {
  el.innerHTML = '<p>我写的代码从来不会报错！</p>';  
} else {
  console.log('节点还没渲染出来');
}


代码块1234567
```

或者使用 `try ... catch ...` 。

```js
var el = document.querySelector('#dfsafds');

try {
  el.innerHTML = '<p>我写的代码从来不会报错！</p>';
} catch (err) {
  console.error(err);
  console.log('节点还没渲染出来');
}


代码块12345678
```



## 4. 小结

操作 DOM 是前端程序员的基本功，也是编写网页的重要知识之一。

获取 DOM 节点的方法有很多，部分方法返回的是 `NodeList` 或 `HTMLCollection` 类型，而不是数组，不能像操作数组一样操作这些集合，转换成数组可以更方便的利用数组的原生方法对其进行操作。

操作节点的时候，特别是动态渲染的节点，需要做空判断，防止程序报错中断执行。