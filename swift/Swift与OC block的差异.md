### Swift与OC block的差异

推荐来源：[weiminghuaa](https://github.com/weiminghuaa)

**Bug现象**

原生和web、小程序、flutter等等交互时，传递给原生的是方法名和数据，所以经常需要写方法转发函数，用到performSelector。在OC时，传递block没问题，Swift就不行，可能在performSelector闪退，也可能在block执行的地方闪退

![21617687306_ pic_hd](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7a2a88f757ec4e9ab78e70a552178c16~tplv-k3u1fbpfcp-zoom-1.image)

![271617690340_ pic_hd](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a368ed191d3e4b4a9ac274deee101c9a~tplv-k3u1fbpfcp-zoom-1.image)

**解决方案**

swift调用performSelector传参之前，将swift的clourse，显示的转换为oc的block

```swift
let block : @convention(block) (Any, Bool) -> () = callback
复制代码
```

[stackoverflow.com/questions/2…](https://stackoverflow.com/questions/26374792/difference-between-block-objective-c-and-closure-swift-in-ios)

**Bug解释**

知识点太偏了，难搞。

解题思路记一下：（真正的技术群很关键，讨论才有灵感） 1、刚开始，完全不知所措

2、在开发者群里好友的建议下，分别写了oc和swift的demo，确认oc没问题，swift有问题

3、基于第二点的结果，猜测，swift的closure和oc的block，虽然都是闭包，但毕竟是不同语言，应该是不同实现，大多数情况在项目中通用，但是具体到这里，swift调oc的runtime去传参，把closure传过去，就出问题，无法copy，closure直接在函数结束时销毁了

4、尝试了解block的底层，并了解closure和block的差异，最终找到了可以显示转换的方法


作者：zhangferry
链接：https://juejin.cn/post/6950085396512374820
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。