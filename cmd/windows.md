** CTRL + R **

sysdm.cpl 系统属性
services.msc 服务
mstsc 远程
taskmgr 任务管理器
regedit 注册表
sysdm.cpl 系统属性


** CMD **

sc delete servicename 删除servicename服务

Run command line "mvn clean package -DskipTests" in directory "source"
Run command line "gradlew clean customizeCamp -PenvironmentName=local --rerun-tasks" in directory "build\camp-dist"

gradlew jmGui -PenvironmentName=qa1    jMeter
gradlew customizeEI     build ESB EI


** VS CODE **

Ctrl + M + M: 折叠或者展开当前方法
Ctrl + M + L:  展开所有方法
Alt + Q: 选择语言模式


** GIT START UP **

git config –global user.name "用户名"
git config –global user.email "邮箱"

ssh-keygen –t rsa –C "邮箱地址"    注意ssh-keygen之间是没有空格的,其他的之间是有空格的
ssh –T git@github.com  测试

git init

git pull

a) 执行增加命令，如下：git add -A
b) 执行提交命令，如下：git commit –m ""
c) 执行推送命令，如下：git push 

常用命令：
  - cat readme.txt 查看文件内容
  - git diff index.html 查看修改内容




