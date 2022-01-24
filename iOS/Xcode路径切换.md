````
#### 问题描述: xcode-select: error: tool 'xcodebuild' requires Xcode, but active developer

#### 解决方案:
> 1.查看当前路劲
```
命令行: xcode-select --print-path

输出: /Library/Developer/CommandLineTools
```

> 2.设置xcode-select到指定位置
```
sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer/ 
```

> 3.查看是否修改成功
```
命令行: xcode-select --print-path

输出: /Applications/Xcode.app/Contents/Developer
````



```

1.Xcode证书路径：
~/Library/MobileDevice/Provisioning Profiles

2.Jenkines共享证书路径：
/用户/共享/Jenkins/Library/MobileDevice/Provisioning Profiles

3.Xcode编译项目缓存垃圾的目录：
~/Library/Developer/Xcode/DerivedData

4.Xcode PCH 根文件路径：
$(PROJECT_DIR)/$(PROJECT_NAME)/

5.Xcode插件路径：
~/Library/Application\ Support/Developer/Shared/Xcode/Plug-ins -name

6.配置文件路径
~/Library/MobileDevice/Provisioning Profiles

7.支持iPhone系统包路径
/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/DeviceSupport
```

