## 深入浅出OC中的block

>  开发中block用了不少，平时只要知道定义block类型的property时要使用copy关键字，然后就是要注意和`__block`和`__weak`关键字的使用场景，注意循环引用的问题就够了。今闲暇之余，总结下对block的深入理解。

### 场景展示

首先我们看如下代码：

```objective-c
NSInteger globalNum = 1;
static NSInteger globalStaticNum = 1;
int main(int argc, char *argv[]) {
    @autoreleasepool {
        NSInteger num = 1;
    		static NSInteger staticNum = 1;
    		__block NSInteger blockNum = 1;
    
    		NSMutableArray *arr = [NSMutableArray arrayWithArray:@[@1,@2,@3]];
    		void (^block)(void) = ^(void) {
        		NSLog(@"局部变量: %ld", num);
        		NSLog(@"静态变量: %ld", staticNum);
        		NSLog(@"全局变量: %ld", globalNum);
        		NSLog(@"全局静态变量: %ld", globalStaticNum);
          	NSLog(@"block修饰变量: %ld", blockNum);
        		[arr addObject:@5];
        		NSLog(@"数组: %@", arr);
        		globalNum = 3;
        };
    
    		num = 2;
    		staticNum = 2;
    		globalNum = 2;
    		globalStaticNum = 2;
    		blockNum = 2;
    		[arr addObject:@4];
    		arr = nil;
   
    		block();
    }
    return 0;
}
```

代码流程图：

<img src="%E6%B7%B1%E5%85%A5%E6%8E%A2%E7%B4%A2OC%E4%B8%AD%E7%9A%84block.assets/%E6%88%AA%E5%B1%8F2020-07-24%20%E4%B8%8B%E5%8D%885.14.52.png" alt="截屏2020-07-24 下午5.14.52" style="zoom:67%;" />

我们在调用block之前，修改了所有定义的变量的值，然后再执行block。不同的变量定义方式，他们的结果会有什么不同呢？

执行程序控制台打印如下：

```objective-c
局部变量: 1
局部静态变量: 2
全局变量: 2
全局静态变量: 2
block修饰变量: 2
```

可以发现除了`定义的局部变量`还是最初定义block时候的值，其他定义类型的变量的值都变成了定义block之后修改的值。

### block捕获

我们打开控制台，cd到当前代码文件所处路径下(我的项目这段代码写在main.m中)，执行`clang -rewrite-objc main.m`。此时会生成main.cpp文件，我们打开main.cpp, 可以看到我们定义的main方法编译成了如下样子：

```objective-c
int main(int argc, char *argv[]) {
    /* @autoreleasepool */ { __AtAutoreleasePool __autoreleasepool; 
        NSInteger num = 1;
        static NSInteger staticNum = 1;
        __attribute__((__blocks__(byref))) __Block_byref_blockNum_0 blockNum = {(void*)0,(__Block_byref_blockNum_0 *)&blockNum, 0, sizeof(__Block_byref_blockNum_0), 1};
        NSMutableArray *arr = ((NSMutableArray * _Nonnull (*)(id, SEL, NSArray<ObjectType> * _Nonnull))(void *)objc_msgSend)((id)objc_getClass("NSMutableArray"), sel_registerName("arrayWithArray:"), ((NSArray *(*)(Class, SEL, ObjectType  _Nonnull const * _Nonnull, NSUInteger))(void *)objc_msgSend)(objc_getClass("NSArray"), sel_registerName("arrayWithObjects:count:"), (const id *)__NSContainer_literal(3U, ((NSNumber *(*)(Class, SEL, int))(void *)objc_msgSend)(objc_getClass("NSNumber"), sel_registerName("numberWithInt:"), 1), ((NSNumber *(*)(Class, SEL, int))(void *)objc_msgSend)(objc_getClass("NSNumber"), sel_registerName("numberWithInt:"), 2), ((NSNumber *(*)(Class, SEL, int))(void *)objc_msgSend)(objc_getClass("NSNumber"), sel_registerName("numberWithInt:"), 3)).arr, 3U));
        void (*block)(void) = ((void (*)())&__main_block_impl_0((void *)__main_block_func_0, &__main_block_desc_0_DATA, num, &staticNum, arr, (__Block_byref_blockNum_0 *)&blockNum, 570425344));
        num = 2;
        staticNum = 2;
        globalNum = 2;
        globalStaticNum = 2;
        (blockNum.__forwarding->blockNum) = 2;
        ((void (*)(id, SEL, ObjectType _Nonnull))(void *)objc_msgSend)((id)arr, sel_registerName("addObject:"), (id _Nonnull)((NSNumber *(*)(Class, SEL, int))(void *)objc_msgSend)(objc_getClass("NSNumber"), sel_registerName("numberWithInt:"), 4));
        arr = __null;
        ((void (*)(__block_impl *))((__block_impl *)block)->FuncPtr)((__block_impl *)block);
    }
    return 0;
}
```

不比纠结过多代码，我们先关注在main.m中定义的block变成了`__main_block_impl_0`类型，定位到其位置代码：

![image-20200727144555778](%E6%B7%B1%E5%85%A5%E6%8E%A2%E7%B4%A2OC%E4%B8%AD%E7%9A%84block.assets/image-20200727144555778.png)

* `__main_block_impl_0`中`__block_impl`我们点击去可以看到有个isa指针。所以block本质上就是个对象，一个将定义的函数以及关联的上下文封装起来的一个对象。

* 我们在block中引用的`num`，`staticNum`，`blockNum`，在这里都被定义成了内部属性.但是并没有发现`globalNum`和`globalStaticNum`
* `num`和`staticNum`还是保留其原来的**NSInteger**类型，但是`blockNum`使用的是``__Block_byref_blockNum_0`类型.

结论如下：

| 变量类型                | block处理方式                                                |
| ----------------------- | ------------------------------------------------------------ |
| 局部变量                | 值捕获，block块外部改变值不会对block内部产生影响             |
| 静态变量                | 指针捕获，block块外部改变值会对block内部产生影响             |
| 全局变量/全局静态变量   | 不捕获，直接取值                                             |
| 使用\_\_block关键字修饰 | 是指针捕获，但是实现不同于静态变量，它会生成一个新的结构体对象。 |

### block形式

block有三种形式，`全局block(__NSGlobalBlock__)`，`栈block(__NSStackBlock__)`，`堆block(__NSMallocBlock__)`

* 全局block存储在初始化data区
* 栈block存储在栈（stack）区
* 堆block存储在堆（heap）区

```objective-c
		NSLog(@"%@", [^(void){
        
    } class]); // 为引用外部变量

    NSLog(@"%@", [^(void){
        NSInteger num = globalStaticNum;
    } class]); // 引用全局静态变量

    NSLog(@"%@", [^(void){
        NSInteger num = globalNum;
    } class]); // 引用全局变量

    static NSInteger temp = 1;
    NSLog(@"%@", [^(void){
        NSInteger num = temp;
    } class]); // 静态变量

    NSInteger number = 1;
    NSLog(@"%@", [^(void){
        NSInteger num = number;
    } class]); // 局部变量

    NSLog(@"%@", [^(void){
        NSInteger num = self.num;
    } class]); // 局部变量

    NSLog(@"%@", [^(void){
        NSInteger num = self.numObj;
    } class]); // 局部变量

		self.block = ^(b1)(void) {
      
    };
		NSLog(@"%@",self.block); // copy全局block

		self.block = ^(b1)(void) {
      id n = self.numObj;
    };
		NSLog(@"%@",self.block); // copy栈block
	
/*
控制台打印如下：
__NSGlobalBlock__
__NSGlobalBlock__
__NSGlobalBlock__
__NSGlobalBlock__
__NSStackBlock__
__NSStackBlock__
__NSStackBlock__
__NSGlobalBlock__
__NSMallocBlock__
*/
```

| 使用方式                     | 结果                   |
| ---------------------------- | ---------------------- |
| 不使用外部变量               | 全局block              |
| 对全局block进行copy操作      | 全局block              |
| 使用外部变量，变量为全局变量 | 全局block              |
| 使用外部变量，变量非全局变量 | 栈block                |
| 对栈block进行copy操作        | 堆block                |
| 对堆block进行copy操作        | 不进行操作，引用计数+1 |

### \_\_block关键字

上文提到，使用关键字修饰的变量，在block中进行指针捕获后并没有定义成原数据类型的指针，而是生成了一个新的结构体对象`__Block_byref_blockNum_0`:

![image-20200727153122992](%E6%B7%B1%E5%85%A5%E6%8E%A2%E7%B4%A2OC%E4%B8%AD%E7%9A%84block.assets/image-20200727153122992.png)

* 可以发现`__Block_byref_blockNum_0`在内部才持有了定义的变量
* 还有一个指向同类型的指针\_\_forwarding;

> 关于forwarding指针：
>
> * forwarding是一个指向自身的指针， 当栈block发生copy操作后，会指向其拷贝的堆block。
> * 所以对block中持有的变量修改，其实修改的是最终指向的那个block。这样保证了访问的值是同样了.

我们可以在回顾下上文代码

* .m文件中：

  ![Jietu20200727-153957](%E6%B7%B1%E5%85%A5%E6%8E%A2%E7%B4%A2OC%E4%B8%AD%E7%9A%84block.assets/Jietu20200727-153957.gif)

* 对应.cpp中实现

  ```objective-c
  __attribute__((__blocks__(byref))) __Block_byref_blockNum_0 blockNum = {(void*)0,(__Block_byref_blockNum_0 *)&blockNum, 0, sizeof(__Block_byref_blockNum_0), 1};
  
  (blockNum.__forwarding->blockNum) = 2; /// 可以看到这并没有直接写成 (blockNum->blockNum) = 2, 而是访问的forwarding指向的block。
  ```

  