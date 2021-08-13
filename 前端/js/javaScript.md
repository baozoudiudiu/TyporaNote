[toc]

### 1.判断数据类型：

使用`typeof`并不能很好的区分`Array，undefined，null`，所以使用`Object.prototype.toString.call`来判断数据类型

```javascript
function isValid(obj, key) {
  return Object.prototype.toString.call(obj) == ('[' + 'object ' + key + ']')
}

/// 是否是有效并且非空的字符串
function isValidString(str) {
  if (typeof(str) === "string" || isValid(str, "String")) {
    return str.length > 0
  }
  return false
}

/// 是否是有效的数字类型
function isValidNum(num) {
  if (typeof(num) === "number" || isValid(num, 'Number')) {
    return !isNaN(num)
  }
  return false
}

/// 是否是有效的布尔类型
function isValidBool(bool) {
  return (typeof(bool) === "boolean" || isValid(bool, 'Boolean'))
}

/// 是否是个空对象或者不是对象类型
function isNotEmptyObj(obj) {
  if (!isValid(obj, 'Object')) {
    return false
  }
  return Object.getOwnPropertyNames(obj).length > 0
}

/// 是否是非空数组
function isNotEmptyArray(arr) {
  if (!isValid(arr, 'Array')) {return false}
  return arr.length > 0  
}
```
---
### 2.指定this

`call`，`apply`，`bind`

```javascript
var obj = {
  log(msg) {
    console.log(this, msg)
  }
}

obj.log('123') /// 这里输出的this，就是obj + 123

var func1 = obj.log
func1('123') /// 这里输出的this不是obj，而是全局global（或者是window）+ 123

// call
func1.call(obj, '123') /// 通过call指定this为obj，输出结果为obj + 123

// apply
func1.apply(obj, '123') /// 通过apply指定this为obj， 输出结果为obj + 123

// bind
var bindFunc = obj.log.bind(obj)
bindFunc('123') /// bind会重新生成一个函数，此函数中的this为bind时传入的this, 这里输出为obj + 123
```

---

### 3.setter、getter

1. 直接在创建对象时设置

   ```javascript
   const student = {
     score: {
       english: 10,
       chinese: 99,
       math: 6,
     },
   
     get totalScore() {
       var score = this.score;
       return score.english + score.chinese + score.math;
     },
   
     set english(value) {
       this.score.english = value;
     },
   
     set chinese(value) {
       this.score.chinese = value;
     },
   
     set math(value) {
       this.score.math = value;
     },
   };
   console.log(student);
   student.math = 66;
   student.chinese = 150;
   student.english = 77;
   console.log(student);
   console.log(student.totalScore);
   ```

2. 通过 `Object.defineProperty` 设置

   ```javascript
   var person = {
     _cash: 1,
     _deposit: 99999,
   };
   
   Object.defineProperty(person, 'money', {
     get: function() {
       return this._cash + this._deposit;
     },
   });
   Object.defineProperty(person, 'cash', {
     set: function(val) {
       console.log('现金发生了改变');
       this._cash = val;
     },
   });
   
   person.cash = 2;
   console.log(person.money);
   ```

---

### 4.javaScript对象的继承

   #### 1.伪继承

父类:

   ```javascript
   // 父类
   function Parent(sender) {
   	this.name = sender.name
   }
   
   Parent.prototype.log = function() {
   	console.log('log', this.name)
   }
   ```

子类:

   ```javascript
   // 子类
   function Sub(sender) {
   	Parent.call(this, sender)
     this.age = sender.age
   }
   
   Sub.prototype = {
     constructor: Sub,
     ...Parent.prototype
   }
   ```

示例：

   ```javascript
   let sender = {name: 'diudiu', age: 18}
   let s = new Sub(sender)
   console.log(s)
   s.log()
   
   /// 控制台输出:
   Sub { name: 'diudiu', age: 18 }
   log diudiu
   ```

接着上面的代码，我们继续添加如下代码：为父类Parent再添加一个方法，并在子类s中调用

   ```javascript
   Parent.prototype.log2 = function() {
     console.log('log2', this.name)
   }
   s.log2()
   ```

可以看到控制台报错如下：

   ```javascript
   TypeError: s.log2 is not a function
   ```

进一步验证：

   ```javascript
   console.log(s instanceof Sub)
   console.log(s instanceof Parent)
   ```

控制台输出如下：

   ```javascript
   true
   false
   ```

综上所述此种方式：

   > 优点：代码简洁。
   >
   > 缺点：并不是真正意义上的继承，原型链上并没有建立起继承的关系。后续如果`Parent.prototype`有添加新方法和属性，`Sub`创建的实例对象是访问不到的。   


#### 2.原型链继承 

创建一个中间对象来实现继承链

父类：

```javascript
// 父类
function Parent(sender) {
	this.name = sender.name
}

Parent.prototype.log = function() {
	console.log('log', this.name)
}
```

子类:

```javascript
// 子类
function Sub(sender) {
	Parent.call(this, sender)
  this.age = sender.age
}
```

创建中间对象，并改写原型链关系

```javascript
// 中间对象
var F = function(){}
// 将其原型对象指向父类原型对象
F.prototype = Parent.prototype
// 将子类的原型对象指向中间对象
Sub.prototype = new F()
// 修改构造方法
Sub.prototype.constructor = Sub
```

至此就完成了，我们可以代码验证一下:

```javascript
let s = new Sub({name: 'diudiu', age: 18})
s.log()
console.log(s instanceof Sub, s instanceof Parent)
```

控制台输出如下：

```javascript
log diudiu
true true
```

我们给父类扩充一个方法, 并通过子类调用:

```javascript
Parent.prototype.log2 = function() {
  console.log('log2', this.name)
}
s.log2()

// 控制台输出
log2 diudiu
```

可以看到，后续`Parent.prototype`有添加新方法和属性，`Sub`创建的实例对象是可以访问到的。 

综上所述：  

>优点：在原型链层面上实现了继承关系。后续 `Parent.prototype`有任何的属性和方法扩展，子类仍然能能够访问到。
>
>缺单：需要创建一个中间对象来实现，要对原型链有一定的了解。

#### 3.通过ES6特性class来实现继承关系

定义父类:

```javascript
class Parent {
	constructor(sender) {
		this.name = sender.name
	}

	log() {
		console.log('log', this.name)
	}
}
```

定义子类：

```javascript
class Sub extends Parent {
	constructor(sender) {
		super(sender)
		this.age = sender.age
	}
}
```

代码验证：

```javascript
let s = new Sub(sender)
console.log(s)
s.log()
console.log(s instanceof Sub)
console.log(s instanceof Parent)
```

控制台输出：

```javascript
Sub { name: 'diudiu', age: 18 }
log diudiu
true
true
```

可以看到子类没有定义log方法，能够访问到父类的log方法。

综上所述：

>优点：代码简洁，容易理解，不需要自己来实现一个中间对象。
>
>缺点：不是所有的主流浏览器都支持ES6的class

---

### 5.遍历对象的key

#### 1.for ... in (遍历可枚举的key, 包括原型上的)

```javascript
let obj = {
  a: 1, b: 2
}
for (let key in obj) {
  console.log(key)
}

// log:
a
b
```

#### 2.Object.keys (遍历可枚举的key，不包括原型上的)

```javascript
let obj = {
  a: 1, b: 2
}
console.log(Object.keys(obj))

// log
['a', 'b']
```

#### 3.Object.getOwnPropertyNames (遍历所有的key，包括可枚举和不可枚举的key, 不包括原型上的)

```javascript
let obj = {a: 1, b: 2}
Object.defineProperty(obj, 'c', {enumerable: false, value: 3})
console.log(Object.getOwnPropertyNames(obj))

// log
[ 'a', 'b', 'c' ]
```

----

### 6.补充

#### 1.hasOwnProperty

想判断枚举出来的这个key是当前对象自己的，还是原型上的，可以通过`hasOwnProperty`来判断。

```javascript
let obj = {a: 1, b: 2}
let newObj = Object.create(obj)
newObj.c = 3
for(let key in newObj) {
	console.log(key, newObj.hasOwnProperty(key))
}

// log
c true
a false
b fals
```

#### 2.创建纯净的对象

`Object.create(null)`创建出来的是一个纯净的对象，它是没有原型的。

