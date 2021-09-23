# 可调用类与Isolates

2020-02-03 23:56 更新

通过实现类的 call() 方法， 能够让类像函数一样被调用。

在下面的示例中，WannabeFunction 类定义了一个 call() 函数， 函数接受三个字符串参数，函数体将三个字符串拼接，字符串间用空格分割，并在结尾附加了一个感叹号。

```dart
class WannabeFunction {
  call(String a, String b, String c) => '$a $b $c!';
}

main() {
  var wf = new WannabeFunction();
  var out = wf("Hi","there,","gang");
  print('$out');
}
```

有关把类当做方法使用的更多信息，请参考 [Emulating Functions in Dart](https://www.dartcn.com/articles/language/emulating-functions) 。



## Isolates

大多数计算机中，甚至在移动平台上，都在使用多核CPU。 为了有效利用多核性能，开发者一般使用共享内存数据来保证多线程的正确执行。 然而， 多线程共享数据通常会导致很多潜在的问题，并导致代码运行出错。

所有 Dart 代码都在隔离区（ isolates ）内运行，而不是线程。 每个隔离区都有自己的内存堆，确保每个隔离区的状态都不会被其他隔离区访问。