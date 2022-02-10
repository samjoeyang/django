
## git从已有目录进行初始化推送

```git
git init //初始化一个git 本地仓库此时会在本地创建一个 .git 的文件夹，一般这个文件夹是隐藏的
git remote add origin https://url //添加远程仓库到本地，url是远程仓库的地址
git pull origin master //如果是初始化推送，那么这一步可以省略
git add . //（. 表示所有的）或者 git add + 文件名 ，将文件保存到缓存区
git commit -m '迁库新建'   //添加文件描述
如果提交的时候因为权限问题失败，可能是需要账号密码：
那么我们可以输入命令：
git config --global user.email "you@example.com"
git config --global user.name “Your Name”
git push origin master //推送到远端的master
```

## 更新单个文件

```git
git fetch

remote: Counting objects: 8, done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 8 (delta 3), reused 8 (delta 3), pack-reused 0
Unpacking objects: 100% (8/8), done.
From github.com:fffy2366/checkout
   cd1768d..2408ca5  master     -> origin/master

git checkout -m 2408ca5 a.txt path/a.txt 
```
