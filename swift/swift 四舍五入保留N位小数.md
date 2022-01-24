给所有的double类型扩展一个新方法.

```
extension Double {

  func roundTo(places: Int) -> Double {

​    let divisor = pow(10.0, Double(places))

​    return (self * divisor).rounded() / divisor

  }

}
```

这样就可以像这样使用了: 3.1415.roundTo(places: 2)

其中rounded用法如下:

```
(5.2).rounded()

// 5.0

(5.5).rounded()

// 6.0

(-5.2).rounded()

// -5.0

(-5.5).rounded()

// -6.0
```

