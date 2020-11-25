# 广汽iOS项目

## 这个项目是混编项目，请仔细阅读本文档后再开发

#### 项目介绍

1. 项目采用SVN管理，软件用的是`Cornerstone`，电脑上已经装好了。打开软件后列表中`GuangQi`下的`IntegratedVersion_1`就是这个项目的远程仓库。
2. 本地项目源码放在桌面上，`IntegratedVersion_1`文件夹就是。
3. 这个项目采用的是原生和React-native混编开发的，iOS项目在`IntegratedVersion_1`下的`iOS`文件夹里。React-native的代码不用管，我们只管iOS的部分就行。
4. 这个项目分`TMS部分`（登录时勾选身份，登录进去就是tms模块）和`WMS部分`（登录时不勾选身份，进去的就是wms模块），TMS部分是采用RN开发的，我们不用惯。WMS部分就是我们自己原生开发的，也是我们需要开发的地方。
5. 这个项目其实分`广汽商贸物流`和`湖南顺捷物流`两个项目，他们其实源码和功能其实一样，只是服务器地址不一样。
6. 所以上架App Store的时候，需要上哪个项目，就改成哪个项目的bundle id，服务器地址，app名称，app图标。

#### 项目相关账号和资料

App Store上架账号：

```
账号：developer007@126.com
密码：Gabc1905@122400
```

##### 广汽商贸物流：

| 描述        |                                                              |      |
| ----------- | ------------------------------------------------------------ | ---- |
| bundle id   | com.guangqi.guangqi.shangmao.lims                            |      |
| 高德地图key | 测试环境：d6e818fcfd9d595469fbdc8990719578<br/>正式环境：e862f6e4308a7b9f84cd146ae5154217 |      |
| 服务器地址  | 测试：http://14.215.45.210:8085 <br/>正式：https://lims.gbl-gz.com |      |
|             |                                                              |      |

##### 湖南顺捷物流：

| 描述        |                                                              |      |
| ----------- | ------------------------------------------------------------ | ---- |
| bundle id   | com.guangqi.guanqi.shunjie.lims                              |      |
| 高德地图key | 测试环境：e469222f949174cec5c296e5aa887d8d<br/>正式环境：2390c9f6201a8ac3e61c9a04c265ca0d |      |
| 服务器地址  | 测试：http://220.169.58.3:2630 <br/>正式:  http://220.169.58.3:2660 |      |
|             |                                                              |      |

#### 上架前准备

1. 修改 bundle id

   1. 上架“广汽商贸”就改成广汽的bundle id， 上架“顺捷”就改成顺捷的bundle id。

2. 修改 app名称

   1. 上架“广汽商贸”就改成`广汽商贸物流`， 上架“顺捷”就改成`湖南顺捷物流。`

3. 修改AppIcon

   1.  项目里appicon有2套，需要哪套就在配置appicon的地方换下配置就好了。
   2. “广汽”的appicon名称为`AppIcon_gq`， “商贸”的appicon名称为`AppIcon_sj`。

4. 修改环境变量

   1. 项目里有个环境变量配置文件`G7.xcconfig`。
   2. 内容如下

   ![截屏2020-11-10 下午2.51.55](%E6%88%AA%E5%B1%8F2020-11-10%20%E4%B8%8B%E5%8D%882.51.55-4991201.png)
   
   注释写得很清楚了，需要上架哪个环境的包就把哪个宏注释给打开，**（记得把其他三个给注释掉）**。

**上面就是修改原生项目的步骤，当然你要是嫌这样子麻烦，你可以自己建两个scheme分别配一套数据，以后就不用来回配置了。**

**接下来就是修改RN的部分代码：**

1. 使用`sublime text`打开项目最外层文件夹`IntegratedVersion_1`
2. 打开`src/Lib/Network`路径下的`ISRequestUrl.js`文件，里面有一项`baseUrl`就是修改服务器地址的地方，根据上架的包修改对应的服务器地址，修改完成记得 cmd + s 保存一下。
3. 打开`src/Lib/Util`路径下的`Global.js`文件，搜索`global.GetLocation = ()`, 里面有个配置高德地图key的地方。请根据不同环境修改成对应的高德key，修改完成后记得 cmd + s 保存一下。

根据上面的步骤弄完之后，打开终端cd到项目根目录下：

```
cd Desktop/IntegratedVersion_1
```

输入如下命令行：

```
react-native bundle --entry-file index.js --bundle-output ./ios/bundle/index.ios.jsbundle --platform ios --assets-dest ./ios/bundle --dev false
```

等待上面命令行执行完成。（修改了内容就会有点耗时，请耐心等待）。

最后一行出现如下文字，就表示命令执行完毕！

```shell
bundle：Done copying assets
```

上面命令行执行完毕之后，运行代码测测没问题，就可以打包上架App Store了。

