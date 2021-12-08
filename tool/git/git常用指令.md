## 本地分支推送到远程

* 远程和本地都有分支，并且有关联（以feature_A分支为例）

```
git push
```

* 远程本地都有分支，但是没有关联（以feature_A分支为例）

```
git push -u origin/feature_A
```

* 远程分支没有，只有本地分支（以feature_A分支为例）

```
git push origin feature_A:feature_A
```

###  拉取本地没有的远程分支到本地

```
git checkout -b 本地分支名 origin/远程分支名
```

### 删除远程分支

```
git push origin --delete [branch name]
```

[branch name]为远程分支名称

### 清除未加入git管理的文件

```
git clean -df
```

### 移除git管理

```
git rm -rf [文件名、路径]
或者
git rm -r --cached (需要删除的路径)
```

### git贮存

工作做了一半,需要切换分支,但是又不想提交.

* 贮存代码

  ```
  git stash save -m'这里写备注'
  ```

* 查看所有的贮存

  ```
  git stash list
  ```

* 恢复到某一贮存点

  ```
  git stash apply (你需要恢复的结点)
  ```

* 删除某一贮存点

  ```
  git stash drop (你需要删除的结点)
  ```

* 恢复到某一贮存点,并立刻删除掉它

  ```
  git stash pop 
  ```

### 修改远程仓库地址

```
git remote set-url origin 新地址
```

### 删除本地项目中远程仓库不存在的分支: 

```
git remote prune origin
```

### 将本地分支推送到远程分支

```git
git push origin <本地分支名>:<远程分支名>
```

### 将本地当前分支推送到远程对应同名分支

```
git push origin <本地分支名>
```

### 将远程分支拉取到本地分支

```
git pull origin <远程分支>:<本地分支>
```

### 将远程指定分支拉取到本地当前分支

```
git pull origin <远程分支>
```



