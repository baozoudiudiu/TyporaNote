[toc]
## 微信小程序原生工程转uni-app工程

我们需要借助插件`miniprogram-to-uniapp`来完成这个需求。

### 1 使用npm安装miniprogram-to-uniapp

```
npm install miniprogram-to-uniapp -g 
```

### 2 检测miniprogram-to-uniapp是否安装成功

```
wtu -V
```

如果有输出版本号，则表示安装成功

### 3 转换工程

```
wtu -i '工程根目录路径'
```

执行该命令，完成后会在同级目录下生成一个转换后的uni-app工程。

### 4 编译运行

运行转换后的项目可能会报错，这个就只能一一排查解决了。目前我没有遇到其他的大问题，唯一遇到的坑点就是之前的原生项目有用到`WeUI`组件。转换成uni-app工程后，运行会报错。

如何在uni-app小程序中使用微信官方组件WeUI，请移步[这里](https://www.jianshu.com/p/01e61b326a7c)

