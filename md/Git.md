[toc]
## git --> 常用命令
> * 1,```git revert [commitID]``` ==> 回退到某个版本而不产生一次提交 
> * 2,```git reset [commitID] [--hard / --soft] ``` ==> 回退到某一个版本,产生一次提交 
>   * --hard : 彻底回退到某个版本,即当前工作区的所有文件都冲洗掉.
>   * --soft : 还是回退到某个版本,但当前工作区的文件还存在,版本的文件在暂存区( stash)
> * 3,```git stash ``` ==> 暂存工作现场
>   * ```git stash pop``` ==>  取出环境.
>   * ```git stash apply stash@{0}``` ==> 也可以取出环境
>   * git stash drop 删除暂存环境
> * 4,```git log --graph ``` ==> 查看分支合并图
> * 5,``` git log -p 文件名 ``` ==> 查看该文件以前的每一次push修改的内容.
> * 6,``` git diff HEAD -- 文件名 ``` ==> 查看某个文件工作区和版本库里最新版本的区别
> * 7,``` git checkout -- 文件名 ``` ==> 把某个文件/夹 在工作区中的所有修改全部撤销
> * 8,``` git branch 分支名 ``` ==> 创建一个分支 
>   * ```git checkout branch1``` ==> 切换分支
>   * ```git switch branch1``` ==> 切换分支 
>   * ```git checkout -b branch1``` ==> 创建并切换至分支 
>   * ```git branch -d branch1``` ==> 删除分支 
>   * ```git branch -D branch1``` ==> 强制删除分支 
> * 9,```git merge branch1 ``` ==> 合并分支 **强烈建议** ```--no-ff```关闭快速合并分支 
>   * ```git merge --no-ff branch1``` ==> 合并后的历史有分支 可能看出曾经做过合并.
>   * ```git rebase branch1``` ==> 也是把 branch1 分支合并到当前分支 
> * 10, ```git remote add origin https://github.com/JasonDu1993/gitskill.git``` ==> 添加远程仓库
> * 11, ```git push <远程主机> <本地分支名> <远程分支名>``` ==> 远程分支名如没有则创建
> * 12,```git push --delete <远程主机> <远程分支> ``` ==> 删除远程分支
> * 13, ```
## git --> 常见问题
> * 1,如果 git push 失败 先git pull 
>   > 如果git push失败，先git pull如果git pull失败，原因是没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接：git branch --set-upstream dev origin/dev，（现在好像改成git branch --set-upstream-to=origin/dev dev）然后在git pull，git push origin master
> * 2,git error: RPC failed; result=22, HTTP code = 411
>   > 解决办法 : 修改 git 的传输字节限制  ==> ```git config http.postBuffer 524288000```
> * 3, error: RPC failed; result=22, HTTP code = 413
>   > fatal: The remote end hung up unexpectedly
> Everything up-to-date
> 这两个错误看上去相似，一个是411，一个是413
> 下面这个错误添加一下密钥就可以了
> 首先ssh-keygen -t rsa -C "abc@bupt.edu.cn"生成密钥