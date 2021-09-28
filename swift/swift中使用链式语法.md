在接触swiftUI时，发现里面的链式语法很方便，coding起来很舒服。如下示例：给image设置属性时无限的使用“点语法”一直“点”下去就好了。

```swift
struct CircleImage: View {
    var body: some View {
        Image("turtlerock")
            .clipShape(Circle())
            .overlay(Circle().stroke(Color.white, lineWidth: 4))
            .shadow(radius: 7)
    }
}
```

相比较之下，在swift中使用UIKit下的控件时，以UITableView为例：

```swift
let tableView = UITableView(frame: CGRect.zero, style: .plain)
tableView.delegate = self
tableView.dataSource = self
tableView.separatorStyle = .none
tableView.showsHorizontalScrollIndicator = false
tableView.showsVerticalScrollIndicator = false
tableView.bounces = false
self.view.addSubview(tableView)
```

每设置一个属性都需要引用一次对象，然后再使用点语法。是否能做到像swiftUI中那样呢？

答案是可以的，我们需要用到`dynamicMemberLookup`来实现这个需求。

```swift
import UIKit

protocol ChainCode {}
extension UIView: ChainCode {}

extension ChainCode {
    public var cc: Chainer<Self> {
        return Chainer(self)
    }
}

@dynamicMemberLookup
struct Chainer<Content> {
    
    public let content: Content
    
    init(_ content: Content) {
        self.content = content
    }
    
    subscript<Value>(dynamicMember keyPath: WritableKeyPath<Content, Value>) -> ((Value) -> Chainer<Content>) {
        var subject = self.content
        return { value in
            subject[keyPath: keyPath] = value
            return Chainer(subject)
        }
    }
}
```

改造后使用如下：

```swift
let tableView2 = UITableView(frame: CGRect.zero, style: .plain)
    .cc
    .separatorStyle(.none)
    .delegate(self)
    .dataSource(self)
    .showsVerticalScrollIndicator(false)
    .showsHorizontalScrollIndicator(false)
    .bounces(false)
    .content
self.view.addSubview(tableView2)
```

`dynamicMemberLookup`相关特性这里不做赘述，具体可查阅[参考链接。](https://github.com/apple/swift-evolution/blob/master/proposals/0252-keypath-dynamic-member-lookup.md)



