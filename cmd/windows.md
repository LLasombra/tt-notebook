**RUN COMMAND**
  - sysdm.cpl 系统属性
  - services.msc 服务
  - mstsc 远程
  - taskmgr 任务管理器
  - regedit 注册表

**CMD**
  - sc delete servicename 删除servicename服务
  - Run command line "mvn clean package -DskipTests" in directory "source"
  - Run command line "gradlew clean customizeCamp -PenvironmentName=local --rerun-tasks" in directory "build\camp-dist"
  - gradlew jmGui -PenvironmentName=qa1    jMeter
  - gradlew customizeEI     build ESB EI

**VS CODE SHORTKEY**
  - Ctrl + M + M: 折叠或者展开当前方法
  - Ctrl + M + L:  展开所有方法
  - Alt + Q: 选择语言模式

**GIT SKILLS**  
1. Global Config  
git config –global user.name "用户名"  
git config –global user.email "邮箱"  
2. UserInfo config  
ssh-keygen –t rsa –C "邮箱地址" `注意ssh-keygen之间是没有空格的,其他的之间是有空格的`  
ssh –T git@github.com  测试  
3. git init
4. git pull

a) 执行增加命令，如下：git add . `不包括被删除的文件` / git add -A `包括被删除的文件`  
b) 执行提交命令，如下：git commit –m ""
c) 执行推送命令，如下：git push origin xxx-branch

**常用命令：**  
  - cat readme.txt 查看文件内容
  - git diff index.html 查看修改内容

**MARKDOWN SYNTAX**
  - `##` 二级标题, `###` 三级标题
  - 段落换行是使用`两个以上空格加上回车`, 或者`一个空行`来表示
  - `*斜体文本*`, `**粗体文本**`, `***粗斜体文本***`
  - `***` 分割线
  - `~~删除线~~`, `<u>带下划线文本</u>`
  - `创建脚注格式类似这样 [^RUNOOB]`
  - 无序列表: `星号(*)、加号(+)或减号(-)`, 有序列表: `数字并加上. 号`来表示, 列表嵌套: 只需在子列表中的选项添加`四个空格`即可
  - 区块引用: 在段落开头使用` > `符号, 后面紧跟一个`空格`
      > 另外区块是可以嵌套的，`一个 > `符号是最外层，`两个 > `符号是第一层嵌套
      > 如果要在列表项目内放进区块，那么就需要在` > 前添加四个空格的缩进`
  - `用``` 包裹一段代码，并指定一种语言（也可以不指定）`
    ```javascript
    $(document).ready(function () {
        alert('TEST');
    });
    ```  
  - 段落上的一个函数或片段的代码可以用反引号把它包起来( ` )
  - 链接: `[链接名称](链接地址)` 或者 `<链接地址>`
      > [菜鸟教程](https://www.runoob.com)
  - 图片: `![alt 属性文本](图片地址)` 或者 `![alt 属性文本](图片地址 "可选标题")`
      > ![RUNOOB 图标](http://static.runoob.com/images/runoob-logo.png)  
      > Markdown还没有办法指定图片的高度与宽度，如果需要可以使用普通的`<img>`标签:  
      > > `<img src="http://static.runoob.com/images/runoob-logo.png" width="50%">`
  - 表格: 表格使用` | `来分隔不同的单元格，使用` - `来分隔表头和其他行
      > `-:`设置内容和标题栏居右对齐, `:-`设置内容和标题栏居左对齐, `:-:`设置内容和标题栏居中对齐  
    
    |  表头  |  表头  | 左对齐 | 右对齐 | 居中对齐 |  
    | :----: | :----: | :----  | ----:  | :----: |  
    | 单元格 | 单元格 | 单元格 | 单元格 | 单元格 |  
    | 单元格 | 单元格 | 单元格 | 单元格 | 单元格 |  
  - 
