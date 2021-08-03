### 判断数据类型：
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
function isEmptyObj(obj) {
  if (!isValid(obj, 'Object')) {
    return true
  }
  for (key in obj) {return false}
  return true
}

/// 是否是非空数组
function isNotEmptyArray(arr) {
  if (!isValid(arr, 'Array')) {return false}
  return arr.length > 0  
}
```
---
### 指定this

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

### setter、getter

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

   ### javaScript对象的继承

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

   优点：代码简洁。

   缺点：并不是真正意义上的继承，原型链上并没有建立起继承的关系。后续如果`Parent.prototype`有添加新方法和属性，`Sub`创建的实例对象是访问不到的。

   

