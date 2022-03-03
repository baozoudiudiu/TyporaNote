[toc]

# 前言

> Dart中的Future就相当于ES6中的Promise，用法也和Promise相似

Dart代码在单线程中执行
代码在运行线程中阻塞的话，会使程序冻结
Future对象（futures）表示异步操作的结果，进程或者IO会延迟完成
在async函数中使用await来挂起执行，直到future完成为止（或者使用then）
在async函数中使用try-catch来捕获异常（或者使用catchError()）
要想同时运行代码，就要为一个web app或者一个worker创建一个isolate

# Future

**Future 的定义**

简单来说，就是我们能够通过它在某个时间点获得异步任务中返回的值。

# Future 的常用函数

- `Future.then()`

  任务执行完成会进入这里，能够获得返回的执行结果。

- `Future.catchError()`

  有任务执行失败，可以在这里捕获异常。

- `Future.whenComplete()`

  当任务停止时，最后会执行这里。

- `Future.wait()`

  可以等待多个异步任务执行完成后，再调用 `then()`。

  只有有一个执行失败，就会进入 `catchError()`。

- `Future.delayed()`

  延迟执行一个延时任务。

- `Future.sync()`

  同步执行

- `Future.microtask()`

  创建一个在微任务队列里运行的Future

示例

```
import 'dart:async';

Future.wait([
  // 2秒后返回结果
  Future.delayed(new Duration(seconds: 2), () {
    return "hello";
  }),
  // 4秒后返回结果
  Future.delayed(new Duration(seconds: 4), () {
    return " world";
  })
]).then((results) {
  // 上面的两个任务执行完毕后进入
  print(results[0]+results[1]);
}).catchError((e){
  // 执行失败会走到这里
  print(e);
}).whenComplete((){
  // 无论成功或失败都会走到这里
});
```

示例

```dart
import 'dart:async';

void main() {
  print("start");
  Future<String> num=Future((){
    return "第一个Future";
  });
  num.then((val)=>print(val));
 
  Future.sync(()=>print("同步执行Futuer"));
  Future.delayed(Duration(seconds: 1), () {
    print("延迟执行Futuer");
  });

  print("end");
}
```

运行结果

> start
> 同步执行Futuer
> end
> 第一个Future
> 延迟执行Futuer

# async/await

- 当调用一个 async 函数时，会返回一个 Future 对象。
- async 函数中可能会有 await 表达式，await表达式会使 async 函数暂停执行，直到表达式中的 Future解析完成后继续执行 async中await后面的代码并返回解决结果。
- `await`只能在`async`中使用。

示例用户信息的存取

```dart
void saveLoginUser(LoginUser user) async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  var loginUserStr = json.encode(user);
  await prefs.setString("loginUser", loginUserStr);
}
Future<LoginUser> getLoginUser() async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  var loginUserStr = prefs.getString('loginUser');
  if (loginUserStr != null) {
    return LoginUser.fromJson(json.decode(loginUserStr));
  } else {
    return null;
  }
}
```