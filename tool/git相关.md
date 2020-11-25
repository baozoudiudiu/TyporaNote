> git clone ... 报错 the remote end hung up unexpectedly

终端输入：

```
git config --global http.postBuffer 500M
git config --global http.maxRequestBuffer 100M
git config --global core.compression 0
```

> 