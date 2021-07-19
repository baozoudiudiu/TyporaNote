## 动态修改class示例

js文件

```js
 data: {
    active: false
  },

  onLoad: function (options) {
    setTimeout(function(){
      this.setData({
        active: true
      })
    }.bind(this), 2000)
  }
```

css文件

```css
.test {
  width: 30rpx;
  height: 30rpx;
  background-color: red;
}

.test-active {
  background-color: blue;
}
```

xml文件

```html
<view class="test {{ active ? 'test-active' : '' }}"></view>
```

> 2秒后，test-active样式会生效

## 动态加载多个class

```html
<view class="content">
  <button bindtap="buttonClickAction">点我啊啊啊啊啊</button>
  <view class="test {{heightActive?'test-height':''}} {{active?'test-active':''}}"></view>
</view>
```

使用多个`{{}}`即可。

