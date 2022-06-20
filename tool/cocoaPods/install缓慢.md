### 终极大招---亲测好用😋

**`pod` 在终端更新慢**
 其实真正慢的原因并不在 **`pod`**命令，而是在于 **`github`**上的代码库访问速度慢，那么就知道真正的解决方案就是要加快 **`git`**命令的速度。

我使用的 **`SS代理`**，默认代理端口为**`1080`**，
 打开**`小飞机`**，配置好代理之后，去终端输入 **`git`**配置命令，命令如下：
 **`git config --global http.https://github.com.proxy socks5://127.0.0.1:1080`**

如此就从根本上解决了问题，下面附上设置代理前后 **`git`**命令的速度

**代理前 10k/s ☹️
 代理后 600k/s** 😍

PS：如果要恢复/移除上面设置的 **`git`**代理，使用如下命令
 **`git config --global --unset http.https://github.com.proxy`**

本文内容参考自`https://blog.csdn.net/wuquan0625/article/details/47401235`有删减😘



```
git config --global http.proxy socks5://127.0.0.1:1086
git config --global http.https://github.com.proxy socks5://127.0.0.1:1086
```

更新的时候，速度可达到1M/S ，更新完，可以直接通过下面的命令恢复

```
git config --global --unset http.proxy
git config --global --unset http.https://github.com.proxy
```