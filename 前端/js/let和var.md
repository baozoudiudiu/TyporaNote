[toc]

### js中let和var区别

#### 1. 作用域不同

* `let`定义的变量作用域仅限于定义该变量的代码块中。比如：if ... else，for...in...，switch...case...等等
* `var`定义的变量作用域为定义该变量的函数范围中（当在函数中定义时），或者为全局的范围（当定义为全局变量时）。

比如以下面一段if条件判断代码为例：

```javascript
(function(){
  if (true) {
    var a = 13
  }
  console.log(a) //控制台输出：13
})()
```

在if代码块内使用`var`定义的变量`b`，在代码块外仍然可以访问，控制台打印出了a的值。

```javascript
(function(){
  if (true) {
    let a = 13
  }
  console.log(a) //控制台输出：ReferenceError: a is not defined
})()
```

当我们将`var`替换成`let`时，在if代码块外访问时，会直接报错。

---

#### 2. 访问顺序的要求不同

* `var`定义变量，可以在未定义前访问。
* `let`定义变量，必须先定义，后访问。

```javascript
(function(){
	console.log(a)
	console.log(b)
	var a = 10
	let b = 11
})()
```

控制台输出：

```javascript
undefined
ReferenceError: Cannot access 'b' before initialization
```

`a`可以在`var`未定义前访问，值为**undefined**，`b`在`let`未定义前访问直接报错。

---

#### 3. 是否可被重复定义

* `let`：同一代码块中，同名变量不可被重复定义。
* `var`：同一作用域下，同名变量可以被重复定义。

还是以if条件语句为例：

let:

```javascript
(function(){
	if (true) {
		let a = 11
		let a = 12
		console.log(a) // 控制台：SyntaxError: Identifier 'a' has already been declared
	}
})()
```

var:

```javascript
(function(){
	if (true) {
		var a = 11
		var a = 12
		console.log(a) // 控制台：12
	}
})()
```

### 结语

笔者的入行语言是`Objective-C`和`swift`，所以认为js中的`let`相比`var`更严谨，也更符合我们的编程思维和习惯。个人更偏向使用`let`而不是`var`。

