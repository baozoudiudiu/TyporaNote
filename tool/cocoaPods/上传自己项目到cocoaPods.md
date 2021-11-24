# iOS：手把手教你发布代码到CocoaPods(Trunk方式)

2016年02月21日 01:18:12

阅读数：247

## **概述**

关于CocoaPods的介绍不在本文的主题范围内，如果你是iOS开发者却不知道CocoaPods，那可能要面壁30秒了。直奔主题，这篇文章主要介绍如果把你的代码发布到CocoaPods代码库中，让别人可以使用“pod search yourOpenProject”命令查找到你的代码。

在2014年5月20日以前，发布代码到CocoaPods可以使用[这篇文章](http://blog.csdn.net/wzzvictory/article/details/20067595)。但时过境迁，出于安全性等方面的考虑，CocoaPods团队放弃了该方式，使用本文要说的trunk方式，用流程图表示如下：（图片来自[CocoaPod官方blog](https://blog.cocoapods.org/)）



下面请跟着我的步伐一步一步往下走，我会告诉你其中的一些坑以及如何应对这些坑：

## **一、注册trunk**

在注册trunk之前，我们需要确认当前的CocoaPods版本是否足够新。trunk需要pod在0.33及以上版本，如果你不满足要求，打开Terminal使用ruby的gem命令更新pod:

| 1    | sudo gem install cocoapods |
| ---- | -------------------------- |
|      |                            |

更新结束后，我们开始注册trunk：

| 1    | pod trunk register zilin_weng@163.com 'weng1250' --verbose |
| ---- | ---------------------------------------------------------- |
|      |                                                            |

邮箱以及用户名请对号入座。用户名我使用的是Github上的用户名。--verbose参数是为了便于输出注册过程中的调试信息。执行上面的语句后，你的邮箱将会受到一封带有验证链接的邮件，如果没有请去垃圾箱找找，有可能被屏蔽了。点击邮件的链接就完成了trunk注册流程。使用下面的命令可以向trunk服务器查询自己的注册信息：

| 1    | pod trunk me |
| ---- | ------------ |
|      |              |

输出如下信息就表示你注册成功，可以进行下面的流程：



## **二、配置PodSpec**

在这一部分中我们需要做两件事：1、为你的代码添加podspec描述文件；2、将podspec文件通过trunk推送给CocoaPods服务器

### **2.1 添加podspec描述文件**

这一步与更换trunk方式前的操作完全一样。什么是podspec描述文件呢？简单地讲就是让CocoaPods搜索引擎知道你的代码的作者、版本号、源代码地址、依赖库等信息的文件。任何支持CocoaPods的开源代码都必须有podspec文件。CocoaPods在github中用一个repo来管理所有支持CocoaPods的开源代码：https://github.com/CocoaPods/Specs。

那如何编写podspec文件呢？官方提供了一个模板并附有非常详细的注释说明。关于podspec文件的编写本文不打算详细讲。强烈建议你看[这篇文章](http://blog.csdn.net/wzzvictory/article/details/20067595)的第三节部分，第四第五节不必看因为已经过时了。

建议直接拿一些成熟的开源库的podspec改就行，生成的模板里有很多冗余的属性。

 

### **2.2 通过trunk推送podspec文件**

现在我们已经有了自己的podspec文件，但是在推送podspec文件之前你需要确认以下几点：

1、确保你的源码已经push到Github上。如果还没push源代码，可以用Terminal cd到本地源代码的根目录，执行：

| 123  | git add -Agit commit -m "first commit for version 1.0.0"git push origin master |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

当然，你也可以使用SourceTree等GUI形式的Git客户端进行代码的推送操作。

2、确保你所push的代码已经打上"version tag"，也就是给源代码打上版本号标签：

| 12   | git tag '1.0.0' git push --tags |
| ---- | ------------------------------- |
|      |                                 |

只有确保了以上两点，CocoaPods才能更准确地找到你的repo。

现在我们开始通过trunk上传你的podspec文件。先cd到podspec文件所在目录，执行(第一次会执行很长的时间...)：

| 1    | pod trunk push WZLBadge.podspec |
| ---- | ------------------------------- |
|      |                                 |

文件名自行对号入座。上面的代码做了三件事：(可以对着文章开头的流程图看)

1、验证你的podspec文件是否合法。在trunk方式之前我们一般用“pod lib lint”命令进行验证。

2、上传podspec文件到trunk服务器(其实最终也会自动添加到https://github.com/CocoaPods/Specs中，只是使用trunk方式省去了以前先fork在pull request的繁琐操作)

3、将你上传的podspec文件转成json格式文件

执行上面的push操作，就相当于你把你的源代码提交给CocoaPods团队审核了，一般需要一到两个工作日可以审核结束。这种心情有点像提交App给Apple审核，哈哈。

*更正：现在CocoaPods审核只需要几秒钟或者几分钟就可以完成了。

 

## **三、更新本地pod依赖**

既然代码提交已经结束，那为什么还要这一步呢？因为你不知道什么时候会审核通过。你可能会说，使用"pod search"命令查一查不就知道了吗？但遗憾的是如果这一步不执行，那在你的电脑上永远不知道代码何时审核通过。举个例子，我在提交了我的一份开源代码[WZLBadge](https://github.com/weng1250/WZLBadge)(截至发稿前已有300+的Star)到pod后的第三天使用search命令仍旧查不到：



这个速度让我觉得不大对劲。于是我使用

| 1    | pod setup |
| ---- | --------- |
|      |           |

命令更新本地pod依赖库后再执行pod search命令(该命令耗时半小时左右，与网速有关)，结果如下：



这证明，代码其实早已经审核通过了！

 

因此，在这一环节中你需要这么做：

在trunk push后，先用"pod search"查找一下你的代码，有结果的话就欢天喜地；没有的话执行"pod setup"进行本地依赖库更新，再search。

------

##  **强势插入：**

如果不出意外，大多数同学在执行上述命令后会卡在“Setting up CocoaPods master repo”这一句中。我的经验是一个字：等！不要关闭Terminal，大概半小时到一小时左右就会完成，提示“Setup completed”。(第一次会比较慢，第一次以后只需要几秒钟即可完成)为什么会卡这么久呢？

pod setup其实在做这么一件事：Cocoapods在将https://github.com/CocoaPods/Specs的信息下载到你电脑的~/.cocoapods目录下并进行文件比对，总数据大小大约在100MB左右，再加上服务器在国外，因此速度会比较慢。在执行过程中你也可以新开一个Terminal窗口，cd到~/.cocoapods目录，用du -sh *来查看下载进度。

当然，如果你有强迫症等不了这么久，那也是有解决方法的。你可以参考唐巧的[这篇文章](http://www.devtang.com/blog/2014/05/25/use-cocoapod-to-manage-ios-lib-dependency/)的“使用CocoaPods的镜像索引”部分，将CocoaPods的镜像地址替换成国内的oschina等服务器地址，速度或许会有提高。但我个人认为没必要，我在没梯子的环境下耗时半小时左右，多点耐心。(第一次会比较慢，第一次以后只需要几秒钟即可完成)

 

------

 

**podspec文件更新方法

有时你可能会遇到这种情况：执行pod trunk push操作后发现podspec文件的某个地方写错了，想更新一下。对于这种情况，我们可能会先尝试着在把podspec文件push一次。但是如果你的代码版本号没变(podspec里的version自然也没变)就会提示push失败，即使你更改了podspec的其他地方，pod也会认为这两个文件是同一个。 我目前为止找不到trunk的相关update接口，所以只能顺水推舟，更新源代码版本号（如：1.1.1->1.1.2），重新push version tag，然后再执行pod trunk push操作。

 

## **写在最后**

trunk的方式的确比以前的fork->pull方式省事很多，但目前网上关于trunk提交CocoaPods代码的资料不多，所以才有了这篇文章。希望这篇文章能各位有一些帮助。

# iOS：手把手教你发布代码到CocoaPods(Trunk方式)

2016年02月21日 01:18:12

阅读数：247

## **概述**

关于CocoaPods的介绍不在本文的主题范围内，如果你是iOS开发者却不知道CocoaPods，那可能要面壁30秒了。直奔主题，这篇文章主要介绍如果把你的代码发布到CocoaPods代码库中，让别人可以使用“pod search yourOpenProject”命令查找到你的代码。

在2014年5月20日以前，发布代码到CocoaPods可以使用[这篇文章](http://blog.csdn.net/wzzvictory/article/details/20067595)。但时过境迁，出于安全性等方面的考虑，CocoaPods团队放弃了该方式，使用本文要说的trunk方式，用流程图表示如下：（图片来自[CocoaPod官方blog](https://blog.cocoapods.org/)）



下面请跟着我的步伐一步一步往下走，我会告诉你其中的一些坑以及如何应对这些坑：

## **一、注册trunk**

在注册trunk之前，我们需要确认当前的CocoaPods版本是否足够新。trunk需要pod在0.33及以上版本，如果你不满足要求，打开Terminal使用ruby的gem命令更新pod:

| 1    | sudo gem install cocoapods |
| ---- | -------------------------- |
|      |                            |

更新结束后，我们开始注册trunk：

| 1    | pod trunk register zilin_weng@163.com 'weng1250' --verbose |
| ---- | ---------------------------------------------------------- |
|      |                                                            |

邮箱以及用户名请对号入座。用户名我使用的是Github上的用户名。--verbose参数是为了便于输出注册过程中的调试信息。执行上面的语句后，你的邮箱将会受到一封带有验证链接的邮件，如果没有请去垃圾箱找找，有可能被屏蔽了。点击邮件的链接就完成了trunk注册流程。使用下面的命令可以向trunk服务器查询自己的注册信息：

| 1    | pod trunk me |
| ---- | ------------ |
|      |              |

输出如下信息就表示你注册成功，可以进行下面的流程：



## **二、配置PodSpec**

在这一部分中我们需要做两件事：1、为你的代码添加podspec描述文件；2、将podspec文件通过trunk推送给CocoaPods服务器

### **2.1 添加podspec描述文件**

这一步与更换trunk方式前的操作完全一样。什么是podspec描述文件呢？简单地讲就是让CocoaPods搜索引擎知道你的代码的作者、版本号、源代码地址、依赖库等信息的文件。任何支持CocoaPods的开源代码都必须有podspec文件。CocoaPods在github中用一个repo来管理所有支持CocoaPods的开源代码：https://github.com/CocoaPods/Specs。

那如何编写podspec文件呢？官方提供了一个模板并附有非常详细的注释说明。关于podspec文件的编写本文不打算详细讲。强烈建议你看[这篇文章](http://blog.csdn.net/wzzvictory/article/details/20067595)的第三节部分，第四第五节不必看因为已经过时了。

建议直接拿一些成熟的开源库的podspec改就行，生成的模板里有很多冗余的属性。

 

### **2.2 通过trunk推送podspec文件**

现在我们已经有了自己的podspec文件，但是在推送podspec文件之前你需要确认以下几点：

1、确保你的源码已经push到Github上。如果还没push源代码，可以用Terminal cd到本地源代码的根目录，执行：

| 123  | git add -Agit commit -m "first commit for version 1.0.0"git push origin master |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

当然，你也可以使用SourceTree等GUI形式的Git客户端进行代码的推送操作。

2、确保你所push的代码已经打上"version tag"，也就是给源代码打上版本号标签：

| 12   | git tag '1.0.0' git push --tags |
| ---- | ------------------------------- |
|      |                                 |

只有确保了以上两点，CocoaPods才能更准确地找到你的repo。

现在我们开始通过trunk上传你的podspec文件。先cd到podspec文件所在目录，执行(第一次会执行很长的时间...)：

| 1    | pod trunk push WZLBadge.podspec |
| ---- | ------------------------------- |
|      |                                 |

文件名自行对号入座。上面的代码做了三件事：(可以对着文章开头的流程图看)

1、验证你的podspec文件是否合法。在trunk方式之前我们一般用“pod lib lint”命令进行验证。

2、上传podspec文件到trunk服务器(其实最终也会自动添加到https://github.com/CocoaPods/Specs中，只是使用trunk方式省去了以前先fork在pull request的繁琐操作)

3、将你上传的podspec文件转成json格式文件

执行上面的push操作，就相当于你把你的源代码提交给CocoaPods团队审核了，一般需要一到两个工作日可以审核结束。这种心情有点像提交App给Apple审核，哈哈。

*更正：现在CocoaPods审核只需要几秒钟或者几分钟就可以完成了。

 

## **三、更新本地pod依赖**

既然代码提交已经结束，那为什么还要这一步呢？因为你不知道什么时候会审核通过。你可能会说，使用"pod search"命令查一查不就知道了吗？但遗憾的是如果这一步不执行，那在你的电脑上永远不知道代码何时审核通过。举个例子，我在提交了我的一份开源代码[WZLBadge](https://github.com/weng1250/WZLBadge)(截至发稿前已有300+的Star)到pod后的第三天使用search命令仍旧查不到：



这个速度让我觉得不大对劲。于是我使用

| 1    | pod setup |
| ---- | --------- |
|      |           |

命令更新本地pod依赖库后再执行pod search命令(该命令耗时半小时左右，与网速有关)，结果如下：



这证明，代码其实早已经审核通过了！

 

因此，在这一环节中你需要这么做：

在trunk push后，先用"pod search"查找一下你的代码，有结果的话就欢天喜地；没有的话执行"pod setup"进行本地依赖库更新，再search。

------

##  **强势插入：**

如果不出意外，大多数同学在执行上述命令后会卡在“Setting up CocoaPods master repo”这一句中。我的经验是一个字：等！不要关闭Terminal，大概半小时到一小时左右就会完成，提示“Setup completed”。(第一次会比较慢，第一次以后只需要几秒钟即可完成)为什么会卡这么久呢？

pod setup其实在做这么一件事：Cocoapods在将https://github.com/CocoaPods/Specs的信息下载到你电脑的~/.cocoapods目录下并进行文件比对，总数据大小大约在100MB左右，再加上服务器在国外，因此速度会比较慢。在执行过程中你也可以新开一个Terminal窗口，cd到~/.cocoapods目录，用du -sh *来查看下载进度。

当然，如果你有强迫症等不了这么久，那也是有解决方法的。你可以参考唐巧的[这篇文章](http://www.devtang.com/blog/2014/05/25/use-cocoapod-to-manage-ios-lib-dependency/)的“使用CocoaPods的镜像索引”部分，将CocoaPods的镜像地址替换成国内的oschina等服务器地址，速度或许会有提高。但我个人认为没必要，我在没梯子的环境下耗时半小时左右，多点耐心。(第一次会比较慢，第一次以后只需要几秒钟即可完成)

 

------

 

**podspec文件更新方法

有时你可能会遇到这种情况：执行pod trunk push操作后发现podspec文件的某个地方写错了，想更新一下。对于这种情况，我们可能会先尝试着在把podspec文件push一次。但是如果你的代码版本号没变(podspec里的version自然也没变)就会提示push失败，即使你更改了podspec的其他地方，pod也会认为这两个文件是同一个。 我目前为止找不到trunk的相关update接口，所以只能顺水推舟，更新源代码版本号（如：1.1.1->1.1.2），重新push version tag，然后再执行pod trunk push操作。

 

## **写在最后**

trunk的方式的确比以前的fork->pull方式省事很多，但目前网上关于trunk提交CocoaPods代码的资料不多，所以才有了这篇文章。希望这篇文章能各位有一些帮助。

笔记:

搜索index路径: ~/Library/Caches/CocoaPods/search_index.json

pods路径: ~/.cocoapods