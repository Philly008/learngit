### Git简介
集中式版本控制系统，版本库是集中存放在中央服务器的。必须要联网才能工作。CVS、SVN即是。  
分布式版本控制系统，每个人的电脑上都是一个完整的版本库。安全性较高。Git即是，不但不必联网，还有强大的分支管理。
### 安装Git
##### Linux上安装Git：
```shell
$ git       # 查看 git是否安装
$ sudo apt-get install git      # 安装 Git

$ tar -zxvf XXX.zip     # 源码安装 git
$ ./config
$ make
$ sudo make install
```
##### Mac 上安装 Git：
直接从 App Store安装 Xcode ，选择菜单“Xcode”>“Preferences”>"Downloads">"Command Line Tools">Install
##### Windows 上安装 Git：
1.在官网https://git-scm.com/downloads 下载并安装；  
2.菜单找到“Git”》“Git Bash”，说明安装成功；  
3.进行登录帐号密码设置：
```shell
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
### 创建版本库（repository）
**Windows中，为了避免遇到各种莫名其妙的问题，请确保目录名不包含中文**
```shell
$ mkdir learngit
$ cd learngit
$ pwd
$ git init  # 把当前目录变成Git可以管理的仓库
$ ls -al    # 显示所有目录文件
```
所有的版本控制系统，只能跟踪文本文件的改动，无法跟踪图片、视频、word等二进制文件的变化。
```shell
# 把文件添加到版本库
$ git add readme.txt
$ git commit -m "wrote readme file"

$ git status    # 查看仓库当前的状态
$ git diff readme.txt   # 查看修改的内容
$ git log --pretty=oneline  # 查看提交历史日志
$ git reset --hard HEAD^    # HEAD 指向当前版本，HEAD^恢复到上个版本，恢复到上上个版本用 HEAD^^，依次累加 ^
$ git reset --hard 1094a    # 恢复到指定ID（可以写ID的部分内容，能唯一识别即可）版本
$ git reflog    # 查看命令历史
```
Git和其他版本控制系统如SVN的一个不同之处就是有暂存区的概念  
工作区（Working Directory）:电脑里能看到的目录，如learngit 就是一个工作区；  
版本库（Repository）：工作区有一个隐藏目录 .git ，这个不算工作区，而是 Git的版本库。  
Git 的版本库有stage（或者叫index）的暂存区、第一个分支master，以及指向master 的一个指针叫HEAD。  
**git add命令实际上就是把要提交的所有修改放到暂存区（stage），然后执行 git commit就可以一次性把暂存区的所有修改提交到分支**  
git 管理的是修改。
```shell
$ git diff HEAD -- readme.txt   # 查看工作区和版本库里面最新版本的区别
$ git checkout -- readme.txt    # 丢弃工作区的修改（用版本库里的版本替换工作区的版本）
$ git reset HEAD readme.txt     # 把暂存区的修改撤销掉（unstage）
$ git rm test.txt   # 从版本库中删除该文件
```
### 远程仓库
```shell
# 1. 创建 SSH Key.在用户主目录下，看看有没有.ssh 目录，如果有，再看看这个目录下有没有 id_rsa 和 id_rsa.pub 这两个文件，如果已经有了，可以直接跳到下一步。如果没有，打开Shell，创建 SSH Key：
$ ssh-keygen -t rsa -C "youremail@example.com"  # 会生成 .ssh 目录及 id_rsa（私钥） 和 id_rsa.pub（公钥） 两个文件
# 2. 登录GitHub，打开“Account settings”>"SSH Keys">"Add SSH Key" ，填上任意 Title，在Key文本框里粘贴 id_rsa.pub 文件的内容。
$ git remote add origin git@github.com:Philly008/learngit.git   # 关联一个远程仓库（Github上已创建一个仓库 learngit）
$ git push -u origin master     # 第一次推送master分支的所有内容。（orgin是Git对远程库默认的叫法）
$ git clone git@github.com:Philly008/learngit.git  # 从远程仓库中克隆一个本地库。
```
Git支持多种协议，包括https，但通过 ssh 支持的原生 git 协议速度最快。
### 分支管理
```shell
$ git branch    # 查看分支
$ git branch dev    # 创建分支 dev
$ git checkout dev  # 切换分支
$ git checkout -b dev   # 创建+切换分支到dev
$ git merge dev  # 合并dev分支到当前分支
$ git branch -d dev     # 删除分支 dev
$ git merge feature1    # 合并，出现冲突时，解决冲突（把Git合并失败的文件手动编辑为期望的内容）后重新提交
$ vim readme.txt    # 修改内容，<<<<<<<，=======，>>>>>>>标记出不同分支的内容
$ git log --graph --pretty=online --abbrev-commit     # 查看分支合并的情况
$ git merge --no-ff -m "merge with no-ff" dev   # 禁用Fast forward 模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息

$ git stash     # 把当前工作现场“储藏”起来，等以后恢复现场后继续工作
$ git stash list     # 查看保存的工作现场
$ git stash pop     # 恢复的同时把stash内容也删除
$ git stash apply stash@{0}     # 恢复到指定的stash

$ git branch -d feature-vulcan  # 无法删除分支时
error: The branch 'feature-vulcan' is not fully merged.
If you are sure you want to delete it, run 'git branch -D feature-vulcan'.
$ git branch -D feature-vulcan  # 加上 -D 参数强制删除
```
### 多人协作
当你从远程仓库克隆时，实际上Git自动把本地的master分支和远程的master分支对应起来了，并且，远程仓库的默认名称是origin。
```shell
$ git remote    # 查看远程库的信息
$ git remote -v # 查看远程库的详细信息
$ git push origin master    # 把本地分支master推送到远程库origin
$ git checkout -b dev origin/dev    # 创建远程origin的dev分支到本地分支dev

$ git push origin dev   # 推送失败时；
$ git pull      # 把最新的提交从 origin/dev抓下来后解决冲突再推送。如果还推送失败；
$ git branch --set-upstream-to=origin/dev dev   # 设置本地dev与远程origin/dev分支的链接，再进行 pull
```
**多人协作的工作模式通常是这样：**  
1. 首先，可以试图用 git push origin <branch-name> 推送自己的修改；      
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用 git pull 试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用 git push origin <branch-name> 推送就能成功！
5. 如果 git pull 提示 no tracking information ，则说明本地分支和远程分支的链接关系没有创建，用命令 git branch --set-upstream-to <branch-name> origin/<branch-name>
```shell
$ git log --graph --pretty=oneline --abbrev-commit
$ git rebase    # 把分叉的提交历史“整理”成一条直线，看上去更直观
```
### 标签管理
```shell
$ git branch    # 查看所有分支
$ git checkout master   # 切换到分支 master
$ git tag v1.0  # 在当前分支上打一个新标签 v1.0
$ git tag   # 查看所有标签
$ git log --pretty=oneline --abbrev-commit  # 查看提交的历史
$ git tag v0.9 f52c622  # 对commit id 为 f52c622的提交打个标签 v0.9
$ git show v0.9     # 查看标签信息
$ git tag -a v0.1 -m "version 0.1 released" f52c622     # -a 指定标签名，-m 指定说明文字

$ git tag -d v0.1   # 删除本地标签v0.1
$ git push origin v1.0  # 推送标签v1.0到远程origin
$ git push origin --tags    # 推送所有未推送到远程的本地标签
$ git tag -d v0.9   # 删除远程标签，需要先删除本地标签
$ git push origin :refs/tags/v0.9   # 再从远程删除
```
**标签总是和某个commit挂钩。如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签**  
**使用GitHub：**
1. 在GitHub上，可以任意Fork开源仓库；
2. 自己拥有Fork后的仓库的读写权限；
3. 可以推送pull request 给官方仓库来贡献代码。

```shell
$ git add -f App.class  # 强制添加到git 
$ git check-ignore -v App.class     # 检查 .gitignore 文件规则
$ git config --global alias.st status   # 命令别名
$ git st    # 等同于 git status
```
忽略某些文件时，需要编写 .gitignore;  
.gitignore 文件本身要放到版本库里，并且可以对 .gitignore 做版本管理。  
忽略文件的原则是：  
1. 忽略操作系统自动生成的文件，比如缩略图等；
2. 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件；
3. 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。  
.gitignore 文件内容类似于：
```shell
# Windows:
Thumbs.db
ehthumbs.db
Desktop.ini

# Python:
*.py[cod]
*.so
*.egg
```












