* 所有变量引用的都是 *对象*，每个对象都是一个 *类* 的实例。数字、函数以及 `null` 都是对象。所有的类都继承于 [Object](https://api.dart.dev/stable/dart-core/Object-class.html) 类。

* class的`私有方法`和`私有属性`使用`_`开头命名。如果您好奇 Dart 为什么使用下划线而不使用诸如 `public` 或 `private` 作为修饰符，请参阅 [SDK 议题 #33383](https://github.com/dart-lang/sdk/issues/33383)

* 遵循 [风格建议指南](https://dart.cn/guides/language/effective-dart/design#types) 中的建议，通过 `var` 声明局部变量而非使用指定的类型。

* `==` 运算符判断两个对象的内容是否一样，如果两个字符串包含一样的字符编码序列，则表示相等。

* 可以使用三个单引号或者三个双引号创建多行字符串：

  ```dart
  var s1 = '''
  你可以像这样创建多行字符串。
  ''';
  var s2 = """这也是一个多行字符串。""";
  ```

* 在字符串前加上 `r` 作为前缀创建 “raw” 字符串（即不会被做任何处理（比如转义）的字符串）：

  ```dart
  var s = r'In a raw string, not even \n gets special treatment.';
  // 代码中文解释
  var s = r'在 raw 字符串中，转义字符串 \n 会直接输出 “\n” 而不是转义为换行。';
  ```

* Dart 在 2.3 引入了 **扩展操作符**（`...`）和 **空感知扩展操作符**（`...?`），它们提供了一种将多个元素插入集合的简洁方法。

  ```dart
  var list = [1, 2, 3];
  var list2 = [0, ...list];
  assert(list2.length == 4);
  
  var list;
  var list2 = [0, ...?list];
  assert(list2.length == 1);
  ```

* Dart 还同时引入了 **集合中的 if** 和 **集合中的 for** 操作，在构建集合时，可以使用条件判断 (`if`) 和循环 (`for`)。

  ```dart
  var nav = [
    'Home',
    'Furniture',
    'Plants',
    if (promoActive) 'Outlet'
  ];
  
  var listOfInts = [1, 2, 3];
  var listOfStrings = [
    '#0',
    for (var i in listOfInts) '#$i'
  ];
  assert(listOfStrings[1] == '#1');
  ```

* 语法 `=> *表达式*` 是 `{ return *表达式*; }` 的简写， `=>` 有时也称之为胖箭头语法。

* `..` 语法称之为 [级联调用](https://dart.cn/guides/language/language-tour#cascade-notation-)。使用级联访问可以在一个对象上执行多个操作

  ```dart
  querySelector('#sample_text_id')
      ..text = 'Click me!'
      ..onClick.listen(reverseText);
  ```

* `~/`除并取整，`%`取余。

* is is! as

  | `as`  | 类型转换（也用作指定 [类前缀](https://dart.cn/guides/language/language-tour#specifying-a-library-prefix))） |
  | ----- | ------------------------------------------------------------ |
  | `is`  | 如果对象是指定类型则返回 true                                |
  | `is!` | 如果对象是指定类型则返回 false                               |

* *表达式 1* ?? *表达式 2*：如果表达式 1 为非 null 则返回其值，否则执行表达式 2 并返回其值。

  ```dart
  /// egg
  String playerName(String name) => name ?? 'Guest';
  
  /// egg
  var count;
  ...
  count ??= 1;/// 如果count为null， 则会被赋值成1
  ```

* 异常

  ```dart
  /// 会抛出异常的方法
  void distanceTo(Point other) => throw UnimplementedError();
  
  /// 捕获异常
  try {
    breedMoreLlamas();
  } on OutOfLlamasException {
    buyMoreLlamas();
  }
  
  try {
    breedMoreLlamas();
  } on OutOfLlamasException {
    // 指定异常
    buyMoreLlamas();
  } on Exception catch (e) {
    // 其它类型的异常
    print('Unknown exception: $e');
  } catch (e) {
    // // 不指定类型，处理其它全部
    print('Something really unknown: $e');
  }
  
  /// 使用rethrow抛出去
  void misbehave() {
    try {
      dynamic foo = true;
      print(foo++); // 运行时错误
    } catch (e) {
      print('misbehave() partially handled ${e.runtimeType}.');
      rethrow; // 允许调用者查看异常。
    }
  }
  
  void main() {
    try {
      misbehave();
    } catch (e) {
      print('main() finished handling ${e.runtimeType}.');
    }
  }
  
  /// 可以使用 finally 语句来包裹确保不管有没有异常都执行代码，如果没有指定 catch 语句来捕获异常，则在执行完 finally 语句后再抛出异常：finally 语句会在任何匹配的 catch 语句后执行：
  try {
    breedMoreLlamas();
  } catch (e) {
    print('Error: $e'); // 先处理异常。
  } finally {
    cleanLlamaStalls(); // 然后清理。
  }
  ```

* 记住构造函数是不能被继承的，这将意味着子类不能继承父类的命名式构造函数，如果你想在子类中提供一个与父类命名构造函数名字一样的命名构造函数，则需要在子类中显式地声明。

* #### Getter 和 Setter

  ```dart
  class Rectangle {
    double left, top, width, height;
  
    Rectangle(this.left, this.top, this.width, this.height);
  
    // 定义两个计算产生的属性：right 和 bottom。
    double get right => left + width;
    set right(double value) => left = value - width;
    double get bottom => top + height;
    set bottom(double value) => top = value - height;
  }
  ```

* #### 指定库前缀

  ```dart
  import 'package:lib1/lib1.dart';
  import 'package:lib2/lib2.dart' as lib2;
  
  // 使用 lib1 的 Element 类。
  Element element1 = Element();
  
  // 使用 lib2 的 Element 类。
  lib2.Element element2 = lib2.Element();
  ```

* #### 导入库的一部分

  ```dart
  // 只导入 lib1 中的 foo。(Import only foo).
  import 'package:lib1/lib1.dart' show foo;
  
  // 导入 lib2 中除了 foo 外的所有。
  import 'package:lib2/lib2.dart' hide foo;
  ```
  
* 使用 `deferred as` 关键字来标识需要延时加载的代码库：
  
  ```dart
  import 'package:greetings/hello.dart' deferred as hello;
  
  /// 当实际需要使用到库中 API 时先调用 loadLibrary 函数加载库：
  Future greet() async {
    await hello.loadLibrary();
    hello.printGreeting();
  }
  ```
  
* ### **要** 使用 `whereType()` 按类型过滤集合。

  假设你有一个 list 里面包含了多种类型的对象， 但是你指向从它里面获取整型类型的数据。 那么你可以像下面这样使用 `where()` ：

  ```dart
  var objects = [1, "a", 2, "b", 3];
  var ints = objects.where((e) => e is int);
  ```

  这个很罗嗦，但是更糟糕的是，它返回的可迭代对象类型可能并不是你想要的。 在上面的例子中，虽然你想得到一个 `Iterable<int>`，然而它返回了一个 `Iterable<Object>`， 这是因为，这是你过滤后得到的类型。

  有时候你会看到通过添加 `cast()` 来“修正”上面的错误：

  ```dart
  var objects = [1, "a", 2, "b", 3];
  var ints = objects.where((e) => e is int).cast<int>();
  ```

  代码冗长，并导致创建了两个包装器，获取元素对象要间接通过两层，并进行两次多余的运行时检查。 幸运的是，对于这个用例，核心库提供了 `whereType()`][where-type](https://api.dartlang.org/stable/dart-core/Iterable/whereType.html) 方法：

  ```dart
  var objects = [1, "a", 2, "b", 3];
  var ints = objects.whereType<int>();
  ```

  使用 `whereType()` 简洁， 生成所需的 [Iterable](https://api.dartlang.org/stable/dart-core/Iterable-class.html)（可迭代）类型， 并且没有不必要的层级包装。

  

  

```dart
var a = 1; /// 自动识别变量类型
num a = 1; /// 声明变量类型
final a = 1; /// final 只能被赋值一次
const int a = 1; /// 使用const 定义的常量是需要在编译阶段即可确定的值，而这个值一旦确定就不能再变化，否则会报错
dynamic a = 1; /// 相当于Objective-c中的id类型， swift中的Any类型
```

