### 方法一：

* 在`main.dart`文件中创建App时将`MaterialApp`替换成`CupertinoApp`。

### 方法二：

* 跳转页面时用如下方法：

  ```dart
  Navigator.push(context, CupertinoPageRoute(builder: (ctx){
  	return 需要跳转的页面;
  }));
  ```

  即：采用`CupertinoPageRoute`。

### 方法三：

* 直接设置全局主题，修改主题中页面切换的方式，具体代码如下：

  ```dart
  class MyApp extends StatelessWidget {
     @override
    Widget build(BuildContext context) {
      return ScreenUtilInit(
        designSize: const Size(375.0, 667.0),
        builder: () {
          return MaterialApp(
            navigatorObservers: [CWRouteListenWidget.routeObserver],
            debugShowCheckedModeBanner: false,
            title: 'flutter_module',
            theme: ThemeData(
              primarySwatch: Colors.amber,
              pageTransitionsTheme: PageTransitionsTheme(
                builders: <TargetPlatform,PageTransitionsBuilder>{
                  TargetPlatform.iOS:createTransition(),
                  TargetPlatform.android:createTransition()
                }
              )
            ),
            home: RootPage(),
            // home: TempPage(),
            routes: RouteManager.routes,
          );
        },
      );
    }
  
    PageTransitionsBuilder createTransition() {
       return CupertinoPageTransitionsBuilder();
    }
  }
  ```

  设置`ThemeData`中的`pageTransitionsTheme`属性，返回`CupertinoPageTransitionsBuilder`即可。