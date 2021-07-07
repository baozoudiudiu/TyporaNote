## UITableView在grouped模式下，去掉组group分割线

> 给cell自定义backgroundView即可

```objective-c
UIView *view= [[UIView alloc] init];
[cell setBackgroundView: view];
```

