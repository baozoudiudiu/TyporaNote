## swift中实现dispatch_once

在Swift 3.0中原有的Dispatch once已经被废弃了.

我们可以通过给DispatchQueue实现一个扩展方法来实现原有的功能：

```
extension DispatchQueue {
    private static var _oneToken = [String]()
    
    class func once(token: String = “\(#file):\(#function):\(#line)”, block: ()->Void) {
        objc_sync_enter(self)
        
        defer
        {
            objc_sync_exit(self)
        }

        if _onceToken.contains(token)
        {
            return
        }

        _onceToken.append(token)
        block()
    }
}
```



