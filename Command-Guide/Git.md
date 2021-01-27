**GIT SKILLS**  
> [Download](https://npm.taobao.org/mirrors/git-for-windows/)
1. Global Config  
git config --global user.name "用户名"  -> git config --global user.name "LLasombra"  
git config --global user.email "邮箱"   -> git config --global user.email "minglin.tang@icloud.com"  
git config --list 查看配置信息
2. UserInfo config  
ssh-keygen -t rsa -C "邮箱地址" `注意ssh-keygen之间是没有空格的,其他的之间是有空格的`  
cd ~/.ssh  
cat id_rsa.pub  
ssh -T git@github.com  测试  
3. git init
4. git pull
5. git branch -D branchName 删除本地分支
6. git push origin --delete branchName 删除远端分支
7. git reset --mixed 21ec4bcc781b65fed901c1e671687040e793ec72 .\Migrations\TableOperationDbContextModelSnapshot.cs 将指定文件回退到指定版本
8. 在一台电脑兼容GitHub和GitLab: [文章1](https://www.cnblogs.com/dennyzhangdd/p/10607472.html), [文章2](https://zhuanlan.zhihu.com/p/34405577)
    > ssh-keygen -t rsa -C "email地址"   -f github    其中-C 后面的是注册github时用的邮箱，-f 后面是生成秘钥的名称
    ``` conf
    # gitlab
    Host git.augmentum.com.cn
    User timothy.tang
    HostName git.augmentum.com.cn
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa

    # github
    Host github.com
    User LLasombra
    Hostname github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/github
    Port 443
    ```
9. push 提示输入密码,可使用以下命令解决: git config --global credential.helper store
10. git checkout -b 本地分支名 origin/远程分支名  从远程仓库里拉取一条本地不存在的分支

a) 执行增加命令，如下：git add . `不包括被删除的文件` / git add -A `包括被删除的文件`  
b) 执行提交命令，如下：git commit -m ""
c) 执行推送命令，如下：git push origin xxx-branch

**常用命令：**  
  - cat readme.txt 查看文件内容
  - git diff index.html 查看修改内容
