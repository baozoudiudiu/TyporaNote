# 你想知道得Cocoapod podflie 引用库的方式都在这里

### Cocoapods库的方式

- 本地库
- 上传到Cocoapods 远程仓库
- 私有库

### Cocoapods 上传官方仓库的引用版本问题

| 操作                       | 说明                |
| :------------------------- | :------------------ |
| pod ‘SwiftyJSON’           | 安装pod最新版本     |
| pod ‘SwiftyJSON’ , ‘4.0’   | 安装指定版本        |
| pod ‘SwiftyJSON’ , ‘> 4.0’ | 安装版本高于4.0     |
| pod ‘SwiftyJSON’ , ‘>=4.0’ | 安装版本高于等于4.0 |
| pod ‘SwiftyJSON’ , ‘< 4.0’ | 安装版本小于4.0     |
| pod ‘SwiftyJSON’ , ‘<=4.0’ | 安装版本小于等于4.0 |

另外一种运算符

| 操作                           | 说明                   |
| :----------------------------- | :--------------------- |
| pod ‘SwiftyJSON’ , ‘~>  0.1.2’ | 版本在[0.1.2  0.2)区间 |
| pod ‘SwiftyJSON’ , ‘~> 0.1’    | 版本在[0.1  1.0)区间   |
| pod ‘SwiftyJSON’ , ‘~> 5’      | 大于或者高于5          |

### Cocoapods 私有库引用方式

- 本地库

| 操作                                              | 说明                    |
| :------------------------------------------------ | :---------------------- |
| pod ‘Alamofire’, :path => ‘~/Documents/Alamofire’ | 指定库路径，找到podspec |

- 私有仓库

| 操作                                                         | 说明                                  |
| :----------------------------------------------------------- | :------------------------------------ |
| pod ‘Alamofire’, :git => ‘https://github.com/Alamofire/Alamofire.git’ | 指定远程仓库路径，默认master 最新节点 |
| pod ‘Alamofire’, :git => ‘https://github.com/Alamofire/Alamofire.git’, :branch => ‘dev’ | 指定分支，默认提交最新节点            |
| pod ‘Alamofire’, :git => ‘https://github.com/Alamofire/Alamofire.git’, :tag => ‘3.1.1’ | 指定版本从tag 节点拉取                |
| pod ‘Alamofire’, :git => ‘https://github.com/Alamofire/Alamofire.git’, :commit => ‘0f506b1c45’ | master 分支，从指定提交节点拉取       |