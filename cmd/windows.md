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

**CHROME SHORTKEY**
  - Ctrl+T 打开新标签页
  - Ctrl+Shift+T 重新打开上次关闭的标签页
  - Ctrl+Tab 或 Ctrl+PgDown 切换到下一个标签页
  - Ctrl+Shift+Tab 或 Ctrl+PgUp 切换到上一个标签页
  - Ctrl+U 查看源代码

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

a) 执行增加命令，如下：git add . `不包括被删除的文件` / git add -A `包括被删除的文件`  
b) 执行提交命令，如下：git commit -m ""
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
  - Others:
    1. 支持HTML元素, 如: `<kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Del</kbd>` --> 使用 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Del</kbd> 重启电脑
    2. 转义：使用`反斜杠`转义特殊字符  
      支持以下这些符号前面加上反斜杠来帮助插入普通的符号:  
        ```
          \   反斜线
          `   反引号
          *   星号
          _   下划线
          {}  花括号
          []  方括号
          ()  小括号
          #   井字号
          +   加号
          -   减号
          .   英文句点
          !   感叹号
        ```
    3. 数学公式, 使用`两个美元符 $$ 包裹 TeX 或 LaTeX 格式`的数学公式来实现,问答和文章页会根据需要加载 Mathjax 对数学公式进行渲染, 如: 
        ```
          $$
          \mathbf{V}_1 \times \mathbf{V}_2 =  \begin{vmatrix} 
          \mathbf{i} & \mathbf{j} & \mathbf{k} \\
          \frac{\partial X}{\partial u} &  \frac{\partial Y}{\partial u} & 0 \\
          \frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0 \\
          \end{vmatrix}
          ${$tep1}{\style{visibility:hidden}{(x+1)(x+1)}}
          $$
        ``` 
    4. typora 画流程图、时序图(顺序图)、甘特图:  [链接](https://www.runoob.com/markdown/md-advance.html)
