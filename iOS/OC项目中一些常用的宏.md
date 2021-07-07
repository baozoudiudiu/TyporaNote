### OC项目中一些常用的宏

> 方法废弃宏 `DEPRECATED_MSG_ATTRIBUTE`

```objective-c
@property (nonatomic, copy) NSString *dogName DEPRECATED_MSG_ATTRIBUTE("use animalName instead");
```

```objective-c
- (void)logDogName:(NSString *)dogName DEPRECATED_MSG_ATTRIBUTE("use logAnimalName: instead");
```

