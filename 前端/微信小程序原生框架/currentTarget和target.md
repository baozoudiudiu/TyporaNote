### DOM事件中的`target`和`currentTarget`

| target        | 触发事件的节点 |
| ------------- | -------------- |
| currentTarget | 处理事件的节点 |

举个例子：

```html
<view id='1' bind:tap='tap1'>
	<view id='2' bind:tap='tap2'></view>
</view>
```

```javascript
tap1: function(e) {
  console.log(e.target, e.currentTarget)
},
tap2: function(e) {
  console.log(e.target, e.currentTarget)
}
```

* 创建了一个父节点，id=1， 绑定了事件：tap1
* 创建了一个子节点，id=2，绑定了事件：tap2

上面我们用不同的id标识了一下两个view，后面我们可以在控制台log中通过id来区分他们。

1. 点击父节点时tap1被触发，此时触发事件的节点和处理事件的节点都是父节点。target和currentTarget中的id都为1。即：`currentTarget == target => 父节点`

   > 综上所述（点击父节点）：
   >
   > tap1中：currentTarget == target => 父节点

2. 点击子节点时先触发tap2, 同理，此时触发事件的节点和处理事件的节点都是子节点，target和currentTarget中的id都为2（`target == currentTarget => 子节点`）。由于事件的冒泡原理，之后会触发tap1，此时触发事件的节点是子节点（因为点击的是节点），而处理事件的是父节点，target的id为2，currentTarget的id为1。（`target => 子节点, currentTarget => 父节点`）

   > 总上所述（点击子节点）：
   >
   > 在tap2中：target == currentTarget => 子节点
   >
   > 在tap1中：target => 子节点, currentTarget => 父节点

