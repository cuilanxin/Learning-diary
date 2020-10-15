<<<<<<< HEAD
git clone 项目地址

git branch -r && a 红色远程 绿色本地

git checkout -b 分支名

git branch 
git add   添加文件
git branch 查看当前属于哪个分支

git branch +名称 创建分支

git checkout +名称 切换分支

git checkout -b +名称 创建并切换分支
git pull   拉代码
git push  推代码
git commit -m""    描述代码内容

ut司机
ug货主

Merge Requests => New merge request('右上角) => 选择自己分支 - 推到dev分支 => 什么都不勾 

## [文章来自](https://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html) 
查看信息
git status  显示有变更的文件
git log 显示当前分支的版本历史
git log --stat 显示commit历史，一级每次commit发生变更的文件
git log -S [内容] 搜索提交历史，根据关键字
git diff 显示暂存区和工作区的差异
git diff --cached[file] 显示暂存区和上一个commit的差异
git diff HEAD 显示工作区与当前分支最新commit之间的差异
git  log -p[file] 显示指定文件每一次diff


查看远程
git remote -v 显示所有远程仓库
git remote show [remote] 显示某个远程仓库的信息
git remote add [shortname] [url] 增加一个新的远程仓库，并命名
git pull [remote] [brnach] 取消远程仓库的变化，并与本地分支合并
git push [remote] [brnach] 上传本地指定分支到远程仓库
git push [remote] --force 强行推送当前分支到远程仓库，即使有冲突
git push [remote] --all 推送所有分支到远程仓库


撤销
git checkout [file] 恢复咱村去到指定文件到工作区
git checkout [commit] [file] 恢复某个commit到指定文件到暂存区和工作区
git checkout . 恢复暂存区所有文件到工作区
git reset [file] 重制暂存区到指定文件，与上一次commit保持一致，但工作区不变
git reset --hard 重置暂存区与工作区，与上一次commit保持一致


其他
git archive 生成一个可供发布到压缩包
=======
git clone 项目地址

git branch -r && a 红色远程 绿色本地

git checkout -b 分支名

git branch 
git add   添加文件
git branch 查看当前属于哪个分支

git branch +名称 创建分支

git checkout +名称 切换分支

git checkout -b +名称 创建并切换分支
git pull   拉代码
git push  推代码
git commit -m""    描述代码内容

ut司机
ug货主

Merge Requests => New merge request('右上角) => 选择自己分支 - 推到dev分支 => 什么都不勾 




>>>>>>> 922357b0727fffcab842694609408bafd93d0ef0
