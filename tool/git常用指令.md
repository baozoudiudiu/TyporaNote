# 本地分支推送到远程

* 远程和本地都有分支，并且有关联（以feature_A分支为例）

`git push`

* 远程本地都有分支，但是没有关联（以feature_A分支为例）

`git push -u prigin/feature_A`

* 远程分支没有，只有本地分支（以feature_A分支为例）

`git push origin feature_A:feature_A`



#  拉取本地没有的远程分支到本地

`git checkout -b 本地分支名 origin/远程分支名`

