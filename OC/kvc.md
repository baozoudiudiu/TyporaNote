### KVC

#### `setValue: forKey:`

当调用`setValue: forKey:`时, 假设传入的`keyPath`为`@"key"`.

赋值的顺序如下:

1. 会去查找是否实现了`setKey:`setter方法,如果实现了则调用该方法.
2. 步骤1不满足, 则查找是否有`_key`成员变量, 如果有则赋值给_key.
3. 步骤2不满足, 则查找是否有`_isKey`成员变量, 如果有则赋值给\_isKey
4. 步骤3不满足, 则查找是否有`key`成员变量, 如果有则赋值给key
5. 步骤4不满足, 则查找是否有`isKey`成员变量, 如果有则赋值给isKey
6. 以上都不满足, 则调用`setValue: forUndefinedKey:`方法

**注:**

* 有一个方法`+(BOOL)accessInstanceVariablesDirectly`默认返回值为`YES`

* 当重写该方法返回`NO`时, 上文中顺序只会执行第1步, 如果第1步不满足则会直接到第6步.

  

#### `valueForKey:`

假设传入的`keyPath`为`@"key"`

查询步骤如下:

1. 查找是否实现getter方法`getKey`, 有则调用
2. 1不满足, 查找是否有成员变量`key`, 有则返回
3. 2不满足, 查找是否有成员变量`isKey`, 有则返回
4. 后续待补充

