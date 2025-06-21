# git学习
## git 推送
### 1.进入到根目录下
### 2.本地仓库建立
将本地目录初始化为Git仓库。默认情况下，初始分支为main
```c
    git init && git symbolic-ref HEAD refs/heads/main

```
### 3.添加远程仓库的SSH URL至本地仓库
```c

   git remote add origin <SSH-URL> 		// 这里使用远程仓库的SSH网址

```
### 4.将本地仓库 与 远程仓库同步一下(防止覆盖远程的最新内容)
```c

    git pull origin main --rebase	// 拉取远程改动并合并到当前分支（使用rebase）

```
### 5.在新的本地仓库中 添加文件到缓存区
```c
    git add <文件名1> <文件名2>	// 添加一个文件
    
    git add .			// 添加该目录下的所有文件
    
    git add <dir>		// 添加制定目录
    
```
### 6.提交 暂存区的文件 至 本地仓库
```c

    git commit -m "添加提交的注释"

```
### 7.验证远程URL是否正确
```c

   git remote -v

```
### 8.推送至 远程仓库【后面只需要推送即可，前面的配置一次即可】
```c

    git push origin main

```
