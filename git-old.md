[toc]
## git --> 初始化
> git 安装完成后初始化一个项目 和 签名
```
//git init 命令把这个目录变成Git可以管理的仓库(repository)
git init
git config --global user.name "xiaobai"
git config --global user.email "mac@easondns.top"
```
> 注意**git config**命令的 **--global**参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。
## git --> 命令
> * git add 文件名 ==>添加到暂存区
> * git config --global user.name 用户名  ==> 设置用户签名(全局)
> * git config --global user.email 邮箱  ==> 用户签名(全局)
> * git init ==> 初始化本地库 (会生成一个.git的配置文件夹)
> * git status ==> 查看本地库状态 
> * git commit -m "日志信息" 文件名 ==> 提交到本地库
> * git log ==> 查看完整历史记录
>   * git log --graph ==> 查看分支合并图
> * git reflog ==> 查看简要历史记录
> * git reset --hard 版本号 ==> 版本穿梭(版本号可在历史记录中查看 )
> * git branch 分支名 ==> 创建分支
> * git branch -v ==> 查看分支 
> * git checkout 分支名 ==> 切换分支
>   * git checkout命令加上-b参数表示创建并切换
>   * git switch -c dev ==> 创建并切换到dev分支
>   * git switch master ==> 切换到master分支 
> * git branch -d dev ==> 删除分支 dev
> * git merge 分支名 ==> 把指定的分支当前的分支上
> * git diff HEAD *** ==> 查看工作区和版本库里面的区别 主要用来对比文件
> * git checkout -- file ==> 文件在工作区的修改全部撤消 如无提交到暂存区,则全部撤消回退到本地库初始版本,如提交到暂存区,则回退到提交后的状态.
> * git rm 文件名 ==> 从版本库中删除 还需要提交 (git commit)
> * git push -u 分支名 ==> 把当前分支推送到远程库 如第一次推送 加上 -u 参数 否 则不用加 -u
> * git clone url ==> 从远程仓库克隆一份到本地
> 
## git --> 流程
> (1) git add * ==> 提交文件到暂存区
> (2) git commit -m "注释的内容" ==> 提交到本地仓库(repository)
> (3) git push 分支名 ==> 把当前的分支推送到远程库(origin) 如远程库是空的,第一次推送的时候要加上 -u参数 

## git --> 问题

> 合并分支时为遇到冲突表现状态为 MERGING
> 状态为 MERGING 时需要处理冲突 执行提交时(git commit)需要注意 **不能带文件名**
> ``` git commit -m "......." ```
> 特殊符号：<<<<<<< HEAD 当前分支的代码 ======= 合并过来的代码 >>>>>>> 分支版本
> * HEAD >当前版本

## git --> .gitignore
