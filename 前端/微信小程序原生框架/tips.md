### 1、自定义组件通讯

核心API：调用`triggerEvent`触发事件给外部。

* 自定义组件内部(test)：

  test.wxml:

  ```html
  <button id='1' bindtap="buttonClick">点我啊</button>
  ```

  test.js:

  ```javascript
  buttonClick: function(e){
    		// 传递给外部的数据
        let detail = {name: 'detail'}
        // 触发此事件的一些选项 (具体解释见下文)
        let options = {bubbles: true, composed: false, capturePhase: false}
        this.triggerEvent('testEvent', detail, options)
  }
  ```

* 外部引用组件：

  index.wxml：

  ```html
  <test bind:testEvent='testClick'></test>
  ```

  index.js：

  ```javascript
  testClick: function(e) {
    console.log(e)
  }
  ```

  上面index.js代码中`e.detail`就能拿到自定义组件test.js中调用`this.triggerEvent('testEvent', detail, options)`中传递过来的`detail`参数。因此，自定义组件中需要传递给外部的数据设置给detail便可。

  至于`options`是一个配置选项，其中可以设置的属性如下表：

  | 选项名       | 类型    | 是否必填 | 默认值 | 描述                                                         |
  | :----------- | :------ | :------- | :----- | :----------------------------------------------------------- |
  | bubbles      | Boolean | 否       | false  | 事件是否冒泡                                                 |
  | composed     | Boolean | 否       | false  | 事件是否可以穿越组件边界，为false时，事件将只能在引用组件的节点树上触发，不进入其他任何组件内部 |
  | capturePhase | Boolean | 否       | false  | 事件是否拥有捕获阶段                                         |

  **”bubbles“**和**”capturePhase“**没什么好说的，这里说一下**”composed“**。composed单独设置成true是不会生效的，需要和bubbles或者capturePhase配置使用。

  index.js:

  ```html
  <test2 id='2' bind:testEvent='testClick2'>
      <test id='1' bind:testEvent='testClick1'></test>
  </test2>
  ```

  test.js:

  ```javascript
  buttonClick: function(e){
        let detail = {name: 'test1'}
        let options = {
          bubbles: true,
          capturePhase: false,
          composed: false
        }
        this.triggerEvent('testEvent', detail, options)
      }
  ```

  

  创建第二个自定义组件**test2**作为**test**的父节点，将**bubbles**设置为true时，test触发事件时，方法调用顺序为：`testClick1 -> testClick2`。

  在test2.wxml中绑定相同的事件：

  ```html
  <view bindtestEvent="viewTap">
    <slot />
  </view>
  ```

  test.js:

  ```javascript
  buttonClick: function(e){
        let detail = {name: 'test1'}
        let options = {
          bubbles: true,
          capturePhase: false,
          composed: true
        }
        this.triggerEvent('testEvent', detail, options)
  }
  ```

  

  将**"composed"**设置为true时，方法的调用顺序为:`testClick1 -> viewTap -> testClick2`

  



