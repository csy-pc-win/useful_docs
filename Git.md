# 常用命令
1. SSH密钥生成方法
   ```
    ssh-keygen -t rsa -C "mail_addr@mail.com"
    ssh-keygen -t rsa -C "username"
    ssh-keygen -t ecdsa -C "username"
   ```
2. 查看配置信息
   
   1).config配置指令
   ```
   git config --global user.name "<username>"
   git config --global user.email <useremail@email.com>
   git config --global color.ui true
   git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
   ```
   2).查看系统config
    ```
     git config --system --list
     git config --global --list
     git config --local --list
    git --version
    ```
3. raw github ip 查询
    ```
    https://www.ipaddress.com/site/raw.githubusercontent.com
    ```
    需要使用wget curl的时候，需要提前打开cmy，否则速度极慢。
    ```
    sudo vim /etc/hosts
    <IP Address> raw.githubusercontent.com
    ```
4.  比较文件差异  
    ```
    git diff <File name>
    ```
5.  比较文件差异 -- 查看工作区和版本库里面最新版本的区别
    ```
    git diff HEAD -- readme.txt
    ```
6.  版本回退
    ```
    git reset --hard HEAD^
    git reset --hard <commit id>
    ```
7.  版本回退 -- 撤销更改
    ```
    git reset HEAD <file>
    ```
    可以把暂存区的修改撤销掉（unstage），重新放回工作区
8.  查看命令历史
    ```
    git reflog
    ```
9.  丢弃工作区的更改
    ```
    git checkout -- readme.txt
    ```
    --很重要，没有--，就变成了“切换到另一个分支”的命令
    (1)自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
    (2)已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

10. 创建 + 切换分支
    ```
    git checkout -b <name>
    git switch -c <name>
    ```
11. 合并分支，保留分支合并历史，打上标签 issue-101
    ```
    git merge --no-ff -m "merged bug fix 101" issue-101
    ```
12. 查看分支合并图
    ```
    git log --graph --pretty=oneline --abbrev-commit
    ```
13. 同时创建本地分支和远程分支
    ```
    git checkout -b dev origin/dev
    ```
14. 查看本地分支
    ```
    git branch
    ```
15. 分支管理策略
    (1)master分支是主分支，因此要时刻与远程同步；
    (2)dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
    (3)bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
    (4)feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

16. 查看远程库的信息
    ```
    git remote
    git remote -v
    ```
17. 向远程仓库推送本地分支
    ```
    git push origin master
    git push origin dev
    ```
18. 错误修复 Error Messages : no tracking information
    方法：建立本地分支和远程分支之间的关联
    ```
    git branch --set-upstream-to <branch-name> origin/<branch-name>
    ```
19. 给最后一个提交的commit创建标签
    ```
    git tag <name>
    ```
20. 给指定提交增加tag
    ```
    git tag <tag-name> <commit id>
    ```
21. dd
    ```
    git show
    ```
22. 删除一个标签
    ```
    git tag -d <tag-name>
    ```
23. 向远程仓库推送一个标签
    ```
    git push origin <tag-name>
    ```
24. 删除远程库中的某个标签
    git push origin :refs/tags/v0.9
25. git stash       ???
26. git stash list  ???
28. git stash apply ???
29. git stash drop  ???
30. git stash pop   ???
31. git cherry-pick ???


# Git开发者工作流程

- 1.  git clone <Repo_URL> -- 从<Repo_URL>处克隆代码
- 2.  git checkout -b <Your_Own_Feature> -- 在Local Git创建一个名为<Your_Own_Feature>的分支，并切换至该分支。
- 3.  按需修改代码
- 4.  git diff  -- 查看在所做的所有修改。
- 5.  git add <Changed_Files1> <Changed_File2> ... <Changed_Filen> -- 暂存所有更改
- 6.  git commit -m "Write your commit here." -- 向Local Git提交更改。
- 7.  git push origin <Your_Own_Feature> -- 向Remote Git推送分支<Your_Own_Feature>及所有更改。
- 8.  检查Remote Git有无内容更新。
  - 1). git checkout main -- 将Local Git的工作分支切换至 main
  - 2). git pull origin main -- 将Remote Git的master分支拉取回来，并与当前分支（即main分支）合并
  - 3). git checkout <Your_Own_Feature> -- 切换至分支<Your_Own_Feature>
  - 4). git rebase main
  - 5). 根据提示进行下一步工作，如提示有冲突，则需手动选择保留的更改。如提示无冲突，则直接进行10.

    Accept Current Change | Accept Incoming Change | Accept Both Changes | Compare Changes

- 9.  git rebase --continue -- 继续进行rebase操作
- 10. git push -f origin <Your_Own_Feature> --
- 11. Make a pull request in the web page of your git server. Notice csy_admin to review codes.


  收到管理者已merge的通知后，应继续执行下述操作：

- 15. git checkout main -- 将Local Git的工作分支切换至 main
- 16. git branch -D <Your_Own_Feature> -- 删除Local Git中的分支<Your_Own_Feature>
- 17. git pull origin master -- 将Remote Git的master分支拉取回来，并与当前分支（即main分支）合并.(Remote Git中的<Your_Own_Feature>被删除。)


## Example 
### Dev A -- Liao

1. git clone ssh://git@192.168.8.106:7022/csy-admin/learn_git_skill.git
2. git checkout -b liao-gitskill
3. 随意修改 
4. git diff
5. git add README.md
6. git commit -m "<Write something here.>"
7. git push origin liao-gitskill
8. 1). git checkout main
   2). git pull origin main
   3). git checkout liao-gitskill
   4). git rebase main
   5). 解决冲突
9. git rebase --continue
10. git push -f origin liao-gitskill
11. Make a pull request in the web page of your git server. Notice csy_admin to review codes.
12. 收到管理者已merge的通知后，应继续执行下述操作：
13. git checkout main
14. git branch -D liao-gitskill
15. git pull origin master
