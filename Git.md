# Git

git init			初始化

git add filename		将修改添加至暂存区

git commit -m "message"		将暂存区的所有修改提交至版本库

git status			查看当前状态

git log				查看版本记录

git reflog			查看命令历史

git checkout filename 		检出文件以撤销工作区修改/切换分支

git reset --hard 版本号		撤销暂存区修改，恢复至工作区

git rm filename			删除文件

git diff			查看修改差异

git branch dev			创建名为 dev 的分支

git checkout master		切换为主分支

git branch -m oldName newName	给分支重命名

git clone			获取一个url对应的远程Git repo, 创建一个local copy.

git remote rm origin 		删除远程仓库的地址

ssh-keygen -t rsa -C "email"	生成ssh密钥

git remote -v			查看远程仓库地址

