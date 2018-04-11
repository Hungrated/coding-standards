# Git

Git是目前世界上最先进的分布式版本控制系统。

参考资料：https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001373962845513aefd77a99f4145f0a2c7a7ca057e7570000

常用命令：

```
# 0 初始化一个git仓库
git init
# 从远程仓库克隆
git clone <repository>

# 提交新文件和提交修改
# 1 添加文件到仓库（工作区 -> 暂存区）
git add <file or dir list>

# 2 把文件提交到仓库（暂存区 -> 版本库）
git commit -m <message>

# 3 推送到远程仓库
git push
```

```
# 查看状态
git status

# 查看具体修改内容
git diff <file>
git diff HEAD -- <file>

# 查看版本日志
git log --graph --pretty=oneline

```

```
# 回退到指定版本
# commitid: HEAD当前版本 HEAD^上一版本 HEAD^^上两个版本 HEAD～100 前100个版本
git reset --hard <commitid>

# 查看git命令记录
git reflog

# 撤销工作区更改
git checkout -- <file>

# 撤销暂存区更改（更改内容回退到工作区）
git reset HEAD <file>

```

```
# 用版本库里的版本替换工作区版本
git checkout -- <file>

# 切换分支
git checkout -b <branchname>

# 查看分支
git branch

# 合并分支
git merge <branchname>

# 删除分支
git branch -d <branchname>

```

```
# 设置别名
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.br branch
git config --global alias.unstage 'reset HEAD'
git config --global alias.last 'log -1'
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```
