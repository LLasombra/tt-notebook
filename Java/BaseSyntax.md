**Setup**
  - [Download JDK](https://www.oracle.com/java/technologies/javase-downloads.html)
  - Config System Environment -> Run -> sysdm.cpl
      > 变量名：JAVA_HOME -> 变量值：C:\Program Files (x86)\Java\jdk1.8.0_91  //要根据自己的实际路径配置
      > 变量名：Path -> 变量值：%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;
      > 变量名：CLASSPATH -> 变量值：.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;  //记得前面有个".", JDK1.5以上可不设置也可以正常编译和运行 Java 程序
  - IDE Download
      > [Eclipse](http://www.eclipse.org/downloads/packages/)
      > [IntelliJ IDEA](https://www.jetbrains.com/idea/download/#section=windows)

**Coding Style**
  - Java: 
      > 大小写敏感
      > 类名: 大写开头，驼峰
      > 方法名: 小写开头，驼峰
      > 文件名: 需与类名相同
  - 标识符: 类名、变量名以及方法名都被称为标识符
      > 大小写字母，美元符($)，下划线(_)，数字(不能用作开头)
      > 大小写敏感，且不能是关键字
  - 修饰符: 用来修饰类中的方法和属性
      > 访问控制修饰符: public > protected > default > private
      > 非访问控制修饰符: final, abstract, static, synchronized
  - 关键字: native, strictfp, transient, volatile, instanceof, assert, synchronized, goto, const

**Class And Object**


**Variable Types**
  - 类变量(静态变量)
    > ddd
  - 实例变量(全局变量)
    > 当对象被实例化之后，每个实例变量的值就跟着确定，在对象创建的时候创建，在对象被销毁的时候销毁
    > 访问修饰符可以修饰实例变量
    > 可以直接通过变量名访问，但在静态方法以及其他类中，就应该使用完全限定名：ObejectReference.VariableName
  - 局部变量
    > 访问修饰符不能用于局部变量
    > 局部变量是在`栈(后进先出)`上分配的
    > 没有默认值，所以被声明后，必须经过初始化才可以使用
  