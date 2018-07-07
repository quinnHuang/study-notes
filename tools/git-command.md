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