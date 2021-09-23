### convariant关键字

```dart
class Animal {
  void chase(Animal x) {}
}

class Mouse extends Animal {}

class Cat extends Animal {
  @override
  void chase(covariant Mouse x) {}
}
```

