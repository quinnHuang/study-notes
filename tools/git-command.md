# Git命令
--------
## 1.配置
配置全局用户名和邮箱
>   
git config **--global** user.name "quinn"  
git config **--global** user.email "quinn@oocl.com"

查看所有配置信息
> git config **--list**

查看某个配置项
> git config **user.name**

忽略文件  
> 在项目目录下直接新建 `.gitignore` 文件，里面编写要忽略的文件名、扩展名、路径等即可。

------
## 2.初始化仓库
初始化仓库有两种做法： 本地初始化和克隆远程仓库
### 2.1本地初始化
将一个目录初始化为git仓库，但是此时目录下的文件还没有添加到版本控制中
> git init

添加文件到stage并提交到repository
>
git add **.**
git commit -m "提交的说明信息"

### 2.2将远程仓库克隆到本地
指定远程仓库的仓库地址进行克隆
> git clone "**https://github.com/Akigaze/GluttonousSnake.git**"

此时会在本地生成一个与远程仓库 **同名** 的目录，该目录即为本地仓库，且目录下的文件已经加入git的版本控制

克隆时指定本地仓库的名称
> git clone "**https://github.com/Akigaze/GluttonousSnake.git**" "**myreponame**"

## 3.免密操作
### https方式
克隆仓库时配置用户的密码  
> https://**user**:**password**@github.com/Akigaze/musicbox.git

查看远程url并设置用户密码
> git remote -v #可以查看目前的url  
git remote set-url origin https://**user**:**password** @github.com/Akigaze/musicbox.git

## 4.分支合并
### 4.1 rebase命令
更改当前分支的根节点，实现分支的合并，相当于提交的迁移
> git rebase **branch-name**

在不指定提交的情况下，默认将当前分支的所有提交都合并到新的节点上  
**解决冲突**：  
1. 当某个提交迁移到新的节点上出现冲突时，就需要解决冲突
2. `git add .`，在解决完之后，存储修改
3. 使用`continue`参数继续执行下一个提交的rebase操作
> git rebase --continue

4. 使用`abort`参数终止rebase的操作，还原当前分支
> git rebase --abort
