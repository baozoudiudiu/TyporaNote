## 深浅拷贝

> 深浅拷贝问题

| 源对象 | 拷贝方式  | 目标对象 | 拷贝类型 |
| --- | --- | --- | --- |
| mutable对象 | copy | 不可变 | 深拷贝 |
| mutable对象 | mutableCopy | 可变 | 深拷贝 |
| immutable对象 | copy | 不可变 | 浅拷贝 |
| immutable对象 | mutableCopy | 可变 | 深拷贝 |
总结: 

1. 可变对象的拷贝都是深拷贝
2. copy出来的都是不可变对象
3. 不可变对象的copy是浅拷贝, mutableCopy是深拷贝
4. @property (nonatomic, copy) NSMutableArray * array;
5. 这样写有什么影响？答: 因为copy方法返回的都是不可变对象，所以array对象实际上是不可变的，如果对其进行可变操作如添加移除对象，则会造成程序crash


