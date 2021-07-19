#### 判断数据类型：
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

/// 是否是对象类型并且属性非空
function isEmptyObj(obj) {
  if (!isValid(obj, 'Object')) {
    return false
  }
  for (key in obj) {return true}
  return false
}

/// 是否是非空数组
function isNotEmptyArray(arr) {
  if (!isValid(arr, 'Array')) {return false}
  return arr.length > 0  
}
```

#### 指定this

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

