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

[参考](https://github.com/apple/swift-evolution/blob/master/proposals/0252-keypath-dynamic-member-lookup.md)

