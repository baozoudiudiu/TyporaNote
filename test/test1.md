# MAC上iTerm 2安装与使用



<img src="http://i1.sinaimg.cn/ent/d/2008-06-04/U105P28T3D2048907F326DT20080604225106.jpg" alt="logo2x.jpg" style="zoom:50%;" />



### 更新日志

- 2018-05-20 [Mac安装powerline 权限问题](https://blog.csdn.net/Mona_233/article/details/54563416)

### 一、前言

iTerm2是MAC下最好用的终端工具，并且还是免费的。iTerm2 是配置完毕开箱即用的 tmux，有标签变色、智能选中等特色功能。在日常开发中，我们难免会与终端命令打交道，比如使用Git，CocoaPods，Homebrew，Hexo等，下面开始介绍自定义终端样式吧！

### 二、目录

> - 下载安装[iTerm 2](http://www.iterm2.com/)
> - 安装powerline
> - 安装oh-my-zsh
> - 安装字体库[fonts](https://github.com/powerline/fonts)
> - 导入配色
> - 主题设置
> - 添加指令高亮效果[zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
> - 快捷键
> - 问题解决

### 三、下载安装[iTerm 2](http://www.iterm2.com/)

- [GitHub](https://github.com/gnachman/iTerm2)

### 四、安装powerline

```
//没有安装pip先安装pip
sudo easy_install pip

//之后安装powerline（这里可能会报错，可以参考问题解决）
pip install powerline-status
复制代码
```

### 五、安装oh-my-zsh

```
curl -L https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh
复制代码
```

### 六、安装字体库[fonts](https://github.com/powerline/fonts)

```
//克隆字体库到本地
git clone https://github.com/powerline/fonts.git

//安装字体
cd fonts
./install.sh
复制代码
```

安装成功之后输出：

```
➜  fonts git:(master) ./install.sh
Copying fonts...
Powerline fonts installed to /Users/WENBO/Library/Fonts
复制代码
```

### 七、导入配色

- 首先到GitHub下载[solarized](https://github.com/altercation/solarized)

```
git clone https://github.com/altercation/solarized
复制代码
```

- 解压zip文件，进入

  solarized/iterm2-colors-solarized

   

  文件，双击

  Solarized Dark.itermcolors

  和

  Solarized Light.itermcolors

  进行安装导入，如下图所示

  ![install-solarized.png](https://user-gold-cdn.xitu.io/2018/5/20/1637e1a0a8980e6e?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

- 进入系统偏好设置，

  profiles

  ->

  Colors

  选择刚刚导入的配色方案即可

  ![屏幕快照 2018-02-12 下午4.07.41.png](https://user-gold-cdn.xitu.io/2018/5/20/1637e1a0a8c30214?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

### 八、主题设置

- 使用[agnoster](https://github.com/fcamblor/oh-my-zsh-agnoster-fcamblor)，下载安装：

```
//克隆主题到本地
git clone  https://github.com/fcamblor/oh-my-zsh-agnoster-fcamblor

//安装主题
cd oh-my-zsh-agnoster-fcamblor
./install
复制代码
```

- 安装成功之后，编辑**~/.zshrc**文件，将**ZSH_THEME**改为**agnoster**

```
# Set name of the theme to load. Optionally, if you set this to "random"
# it'll load a random theme each time that oh-my-zsh is loaded.
# See https://github.com/robbyrussell/oh-my-zsh/wiki/Themes
ZSH_THEME="agnoster"
复制代码
```

### 九、添加指令高亮效果[zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)

- 下载文件

```
//克隆项目到本地
git clone git://github.com/zsh-users/zsh-syntax-highlighting.git
复制代码
```

- 编辑**.zshrc**文件，在最后添加如下内容

```
source /Users/WENBO/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
plugins=(zsh-syntax-highlighting)
复制代码
```

**注意**

```
 /Users/WENBO是*.zshrc文件所在路径，这里替换成你自己的就好了
复制代码
```

- 设置成功之后，效果如下：

  ![屏幕快照 2018-02-12 下午4.55.25.png](https://user-gold-cdn.xitu.io/2018/5/20/1637e1a0a8d66380?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

### 十、快捷键

自己也才安装，先记录下来吧。

|        说明        |                        快捷键                        |
| :----------------: | :--------------------------------------------------: |
|      新建标签      |                     command + t                      |
|      关闭标签      |                     command + w                      |
|      切换标签      |         command + 数字 command + 左右方向键          |
|      切换全屏      |                   command + enter                    |
|        查找        |                      command +f                      |
|      垂直分屏      |                     command + d                      |
|      水平分屏      |                 command + shift + d                  |
|      切换屏幕      | command + option + 方向键 command + [ 或 command + ] |
|    查看历史命令    |                     command + ;                      |
|   查看剪贴板历史   |                 command + shift + h                  |
|     清除当前行     |                       ctrl + u                       |
|       到行首       |                       ctrl + a                       |
|       到行尾       |                       ctrl + e                       |
|      前进后退      |            ctrl + f/b (相当于左右方向键)             |
|     上一条命令     |                       ctrl + p                       |
|    搜索命令历史    |                       ctrl + r                       |
| 删除当前光标的字符 |                       ctrl + d                       |
| 删除光标之前的字符 |                       ctrl + h                       |
| 删除光标之前的单词 |                       ctrl + w                       |
|   删除到文本末尾   |                       ctrl + k                       |
|   交换光标处文本   |                       ctrl + t                       |
|       清屏1        |                     command + r                      |
|       清屏2        |                       ctrl + l                       |

### 十一、问题解决

- [brew link python报错](http://blog.csdn.net/tymatlab/article/details/78609861)

```
sudo mkdir /usr/local/Frameworks
sudo chown $(whoami):admin /usr/local/Frameworks
复制代码
```

之后执行，链接成功

```
brew link python
复制代码
```

- 安装powerline报错**Permission denied**，原因是没有安装python,，通过homebrew安装python

```
brew install python
复制代码
```

- 命令显示？号，如下图所示：

  ![屏幕快照 2018-02-12 下午4.38.27.png](https://user-gold-cdn.xitu.io/2018/5/20/1637e1a0a8a8e24b?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

  解决办法：进入

  Preference

  ->

  Profiles

  ->

  Text

  ，做如下配置即可：

  ![屏幕快照 2018-02-12 下午4.59.18.png](https://user-gold-cdn.xitu.io/2018/5/20/1637e1a0a8f2d04e?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

- Mac安装powerline 权限问题，报错如下

  ![屏幕快照 2018-05-20 下午3.57.18.png](https://user-gold-cdn.xitu.io/2018/5/20/1637e1a0cbe25c05?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

  解决办法：

```
pip install powerline-status --user -U
复制代码
```

### 十二、结语

在掘金上发现了这款终端工具，自己平时也有用到终端工具，于是就尝试给自己的MAC装上这款软件，在安装过程中还是遇到一些问题，不过最后都解决了。如果你也爱好终端命令操作，可以尝试DIY你喜欢的终端样式哦。

### 参考文章

- [iTerm 2 && Oh My Zsh【DIY教程——亲身体验过程】](https://www.jianshu.com/p/7de00c73a2bb)
- [Mac终端iTerm2配置](http://matt33.com/2016/07/09/mac-software/)

关注下面的标签，发现更多相似文章