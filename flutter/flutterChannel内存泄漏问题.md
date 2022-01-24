## iOS和flutter混编FlutterMethodChannel内存泄漏问题

### 1.前言

移动端原生和flutter模块混编时，少不了要在两个模块之间做通讯的需求。flutter为我们提供了三种交互方式：

* [BasicMessageChannel](https://juejin.cn/post/7012954548989853733)：双向通道，iOS和flutter都可以主动向对方传递消息，最简单的传递数据。

* [MethodChannel](https://juejin.cn/post/7012905714418974728)：双向通道，使用方式基本和BasicMessageChannel一样，但是高级一些，能够自定义methodName。

* [EventChannel](https://juejin.cn/post/7012955190580445197)：用于事件流的发送（event streams), 属于持续性的单向通信, 只能是 `iOS` 端主动调用, 常用于传递原生设备的信息, 状态等, 比如电池电量, 远程通知, 网络状态变化, 手机方向, 重力感应, 定位位置变化等等.

具体如何使用可以点击上方对应的链接查阅，这里不再赘述。本篇主要记录我在使用中遇到得一点问题和疑惑。



### 2.版本

当前使用的**flutter**和**dart**版本如下：

```idl
flutter 2.8.1 • channel stable • https://github.com/flutter/flutter.git
Framework • revision 77d935af4d (5 weeks ago) • 2021-12-16 08:37:33 -0800
Engine • revision 890a5fca2e
Tools • Dart 2.15.1
```



### 3.功能描述

很简单的一个测试功能：

* 原生**ViewController**跳转到**flutter**模块，（即，present一个**FlutterViewController**）。
* **flutter模块**点击左上角按钮触发**MethodChannel**，通知原生调用**dismiss**方法关闭flutter模块。

具体代码实现如下（只贴主要代码）：

#### 3.1原生代码

* 为了方便查看对象是否销毁，这里继承一下官方的类，并重写deinit方法。

  ```swift
  class CusFlutterViewController: FlutterViewController {
      override init(engine: FlutterEngine, nibName: String?, bundle nibBundle: Bundle?) {
          super.init(engine: engine, nibName: nibName, bundle: nibBundle)
          self.modalPresentationStyle = .fullScreen
      }
      required init(coder aDecoder: NSCoder) {
          super.init(coder: aDecoder)
      }
      deinit {
          debugPrint("deinit \(self)")
      }
  }
  
  class CusFlutterMethodChannel: FlutterMethodChannel {
      
      deinit {
          debugPrint("deinit \(self)")
      }
  }
  ```

  当**FlutterViewController**和**FlutterMethodChannel**被销毁时，控制台会打印出对应的日志。

* 创建引擎，创建flutterViewContr，methodChannel，并实现回调。

  ```swift
  let flutterEngine = FlutterEngine(name: "my flutter engine")
  flutterEngine.run()
  GeneratedPluginRegistrant.register(with: flutterEngine);
  
  ...省略无关代码
  
  self.flutterVC = CusFlutterViewController.init(engine: flutterEngine, nibName: nil, bundle: nil)
  
  self.channel = CusFlutterMethodChannel.init(name: "channel", binaryMessenger: self.flutterVC!.binaryMessenger)
  
  self.channel?.setMethodCallHandler { [weak self] handler, block in
      let method = handler.method
      switch method {
      case "exit_flutter_module":
          self?.dismiss(animated: true, completion: {
              self?.channel?.setMethodCallHandler(nil)
          		self?.channel = nil
          		self?.flutterVC = nil
          })
      default:()
      }
  }
  
  self.present(self.flutterVC!, animated: true, completion: nil)
  ```

#### 3.2 flutter端代码

点击按钮时，通知原生dismiss掉flutter模块

```dart
const MethodChannel flutterMethodChannel = MethodChannel('channel');

...省略无关代码
  
TextButton(
  child: const Text("back", style: TextStyle(color: Colors.red),),
  onPressed: () async {
    var result = await flutterMethodChannel.invokeMapMethod("exit_flutter_module") ?? {};
    debugPrint("$result");
  },
)
```



### 4.发现问题

当运行上述代码，从flutter模块返回原生页面时，发现控制台仅仅只输出了**flutterViewController**的deinit日志，而`flutterMethodChannel`的`deinit`方法并没有被触发。每次重新进入到flutter页面都会再次创建一个新的channel对象，但是返回时析构函数`deinit`并不会被触发。也就是说我重复N次进入和退出flutter页面时，内存中便创建了N个channel对象，他们都没有被释放掉。

个人具体探索问题的过程，这里就不赘述了，直接说说我的发现吧。将上文中创建channel的代码：

```swift
self.channel = CusFlutterMethodChannel.init(name: "channel", binaryMessenger: self.flutterVC!.binaryMessenger)
```

修改成：

```swift
self.channel = CusFlutterMethodChannel.init(name: "channel", binaryMessenger: self.flutterVC!.binaryMessenger, codec: FlutterStandardMethodCodec.sharedInstance())
```

上述的问题便解决了。从flutter页面返回原生界面时，channel的析构函数触发，控制台日志有输出。

### 5.疑惑

其实看官方注释的意思，两种构造方法方法区别不大：

```objective-c
/**
 * Creates a `FlutterMethodChannel` with the specified name and binary messenger.
 *
 * The channel name logically identifies the channel; identically named channels
 * interfere with each other's communication.
 *
 * The binary messenger is a facility for sending raw, binary messages to the
 * Flutter side. This protocol is implemented by `FlutterEngine` and `FlutterViewController`.
 *
 * The channel uses `FlutterStandardMethodCodec` to encode and decode method calls
 * and result envelopes.
 *
 * @param name The channel name.
 * @param messenger The binary messenger.
 */
+ (instancetype)methodChannelWithName:(NSString*)name
                      binaryMessenger:(NSObject<FlutterBinaryMessenger>*)messenger;

/**
 * Creates a `FlutterMethodChannel` with the specified name, binary messenger, and
 * method codec.
 *
 * The channel name logically identifies the channel; identically named channels
 * interfere with each other's communication.
 *
 * The binary messenger is a facility for sending raw, binary messages to the
 * Flutter side. This protocol is implemented by `FlutterEngine` and `FlutterViewController`.
 *
 * @param name The channel name.
 * @param messenger The binary messenger.
 * @param codec The method codec.
 */
+ (instancetype)methodChannelWithName:(NSString*)name
                      binaryMessenger:(NSObject<FlutterBinaryMessenger>*)messenger
                                codec:(NSObject<FlutterMethodCodec>*)codec;
```

第一个方法其实就是第二个方法**codec**默认为**FlutterStandardMethodCodec**。至于为何第一中方法构造的channel不能释放，只能去看源码才能解惑了。如果大家有好的想法和见解，还请不吝赐教！







