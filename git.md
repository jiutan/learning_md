# git学习
## git 推送
### 1.进入到根目录下
### 2.本地仓库建立
将本地目录初始化为Git仓库。默认情况下，初始分支为main
```c
    git init && git symbolic-ref HEAD refs/heads/main   // 初始化git仓库，并且令当前主分支为main

```
### 3.添加远程仓库的SSH URL至本地仓库
```c
    git remote add origin <SSH-URL> 		// 方法一：这里使用远程仓库的SSH网址

    git clone <HTTPS-URL>                // 方法二：克隆远程仓库

```
#### 若已存在远程库，想更改远程仓库
```c
    // 第一步：查看git对应的远程仓库地址
    git remote -v              
    // 第二步：删除关联对应的远程仓库地址
    git remote rm origin                // origin 是在-v中查看
    // 第三步：查看是否删除成功，如果没有任何返回结果，表示OK
    git remote -v   
    // 第四步：重新关联git远程仓库地址
    git remote add origin "新的仓库地址"
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

    git push origin main       // 需要输入账户和密码时：账户用github的邮箱，密码用Personal Access Tocken

```
## git常用代码（注：省略 [] ）
### 1. git常用代码
```c    
    git log                   // 显示每个提交的详细修改信息

    git log --author="author name"                         // 查看 指定作者author name 的 提交记录
```
### 2. git分支操作：git branch [选项] [分支名称]
```c
/*
    创建分支
*/
    git branch [分支名称]       // 创建 分支

/**
    删除分支    
*/
    git branch -d [分支名称]    // 删除 分支（前提：该分支已经合并，才可以删除。如果没有合并，系统会提示是否强制删除）

    git branch -D [分支名称]    // 强制删除 分支

/*
    查看分支 
*/
    git branch                 // 查看当前 【本地】仓库下的 分支（注意：需要 commit一次才会有）
  
    git branch -v              // 详细查看 分支列表。并且附带 每个分支的最后一次信息。
    
    git branch -a              // 显示查看 【本地和远程】 的所有分支

    git branch -r              // 查看 【远程】 的所有分支

    git branch --merged        // 显示 已经与当前分支合并的所有分支。

    git branch --no-merged     // 显示 当前分支中尚未合并的所有分支。
/*
    切换分支
*/
    git checkout [分支名称]     // 切换 分支

    git checkout -b [分支名称]  // 创建 新分支，并且切换到该分支

/*
    合并分支（注意：该命令是将 其他分支的修改 合并到 当前分支）
*/
    git merge [需要被合并的分支]  // 将 需要被合并的分支 合并到 当前分支 【注意：提前使用 checkout 换到 主分支】

/*
    恢复 某个 文件/版本
*/
    git checkout [文件名字]     // 恢复/撤销 某个文件的修改 

    git checkout [commit_id]   // 恢复 指定id 的历史版本 【 commit_id 在 git log 中查看】

    git checkout [commit_id] [file_name]    // 恢复 指定文件 的 指定id历史版本 【 commit_id 在 git log 中查看】

```
### 3.fetch与pull (通过 git remote -v 查看 远程代码库的名字)：将 远程代码库 更新到 本地代码库
#### fetch：不会自动合并代码
```c
    
    git fetch [远程代码库名字（默认为 origin）]          // 将远程代码库的代码更新到本地代码库，不会自动合并代码。[需要手动执行 git merge 命令]

```
#### pull：如果没有冲突，则 自动提交合的修改
```c

    git pull [远程代码库名字] [要拉取的分支名称（省略则默认：当前分支）]        // 先执行fetch。若有冲突，则需手动解决冲突并提交修改；若无冲突，则自动提交合并的更改。

```