## iOS原生项目中混编flutter代码调试时实现热更新（Hot Reload）

### 1.前言
关于iOS原生项目如何集成flutter请移步：[iOS原生项目通过cocoaPods集成flutter](https://www.jianshu.com/p/f6233350566a)

单纯的运行flutter项目后，修改的代码能通过`hot reload`特性实时的更新到界面上去，提高了开发效率。iOS原生项目就无力吐槽了，想看效果就得重新运行项目（swiftUI除外，但是现在还不普及）。

混编项目中，主体项目还是原生项目所以修改代码之后还是得重新运行起来看效果。但是项目中穿插的flutter模块页面是否能够实现热更新调试呢？答案是可以的，方法见下文。

### 2.原生项目
iOS13还是iOS14之后需要如下配置，具体是哪个版本之后不太记得了，反正配上就完事了。

在`info.plist`中添加如下配置，**右键Info.plist -> Open As -> Source Code**（个人比较喜欢以这种方式打开info.plist）

```
<key>NSBonjourServices</key>
	<array>
		<string>_dartobservatory._tcp</string>
	</array>
<key>NSLocalNetworkUsageDescription</key>
<string>需要访问本地网络权限</string>
```

*  **注意：如果项目中没有本地网络权限等相关业务需求，仅仅只是开发时用来调试flutter模块的情况，请在上架前删掉以上配置，否则审核会被拒。**
*  **如果嫌麻烦，可以单独配置一份debug模式下的info.plist。和release模式下info.plist分开使用，这样就不需要来回的添加和删除了。**

### 3.flutter模块

待原生项目运行成功后，控制台进入到flutter模块的根目录下执行以下命令行:

```
flutter attach
```

看到网上有很多博文说，需要先执行`flutter attach`再运行原生项目才可以。反正我无论是先运行再执行命令行，还是先执行命令行再运行项目，二者都可以。

### 4.补充说明

* 执行完`flutter attach`后会出现：

  `Waiting for a connection from Flutter on xxxxx...`

  如果你出现了报错，一般都是检测到了多设备的报错，根据提示指定一个设备id就可以了。

* 原生项目运行后，进入flutter页面时，会出现如下log：

  ```
  Syncing files to device XXXXXX...                             10.5s
  
  Flutter run key commands.
  r Hot reload. 🔥🔥🔥
  R Hot restart.
  h List all available interactive commands.
  d Detach (terminate "flutter run" but leave application running).
  c Clear the screen
  q Quit (terminate the application on the device).
  ```

  成功后，在控制台输入‘r’为热更新，‘R’为热重载，‘q’退出调试。
