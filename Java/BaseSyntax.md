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
  - 一个源文件只能有`一个public类`, 但可以有`多个非public`类, 并且源文件的名称应该和public类的类名保持一致

**Class And Object**

**DataTypes**
- *Basic DataTypes*
  - byte: 1个字节(8位, 即[-128(-2^7) - 0 - 127(2^7-1)]), 有符号, 用在大型数组中节约空间, 主要代替整数, 默认值 0
  - short: 2个字节, 有符号, 也可以像 byte 那样节省空间, 默认值 0
  - int: 4个字节, 有符号, 一般地`整型变量默认类型`为 int 类型, 默认值 0
  - long: 8个字节, 有符号, 主要使用在需要比较大整数的系统上, 默认值是 0L, "L"理论上不分大小写，但是若写成"l"容易与数字"1"混淆，不易分辩, 所以最好大写
  - float: 4个字节, 有符号, 单精度, 在储存大型浮点数组的时候可节省内存空间, 默认值是 0.0f, 浮点数不能用来表示精确的值，如货币
  - double: 8个字节, 有符号, 双精度, `浮点数的默认类型`为double类型, 默认值是 0.0d, 同样不能表示精确的值，如货币
  - boolean: 只有两个取值：true 和 false, 默认值是 false, 《Java虚拟机规范》给出了4个字节，和boolean数组1个字节的定义，具体还要看虚拟机实现是否按照规范来，所以1个字节、4个字节都是有可能的。这其实是运算效率和存储空间之间的博弈，两者都非常的重要
  - char: 2个字节, 是一个单一的16位Unicode字符, 最小值是 \u0000(即为0), 最大值是 \uffff(即为65,535), 可以储存任何字符(包装类：java.lang.Character)
- 基本类型的取值范围以`常量`的形式定义在对应的`包装类`中, 如: Byte.SIZE(byte的二进制位数), Byte.MIN_VALUE, Byte.MAX_VALUE
- 实际上，JAVA中还存在另外一种基本类型 void，它也有对应的包装类 java.lang.Void，不过我们无法直接对它们进行操作
- byte、short、int和long都可以用十进制、16进制以及8进制的方式来表示。当使用常量的时候，`前缀 0`表示 8 进制，而`前缀 0x`代表 16 进制
- *Reference DataTypes*
  - 对象(如String等)、数组都是引用数据类型
  - 所有引用类型的默认值都是null
  - 一个引用变量可以用来引用任何与之兼容的类型
- Constant
  - 常量在程序运行时是不能被修改的, 使用 final 关键字来修饰常量, 通常使用`大写字母`表示常量
  - 字符串常量和字符常量都可以包含任何Unicode字符。例如：`char a = '\u0001'; String a = "\u0001";`
- 自动类型转换
  - `byte, short, char —> int —> long —> float —> double` 转换从低级到高级
  - 不能对boolean类型进行类型转换
  - 不能把对象类型转换成不相关类的对象
  - 在把容量大的类型转换为容量小的类型时必须使用强制类型转换, 转换过程中可能导致溢出或损失精度
  - 浮点数到整数的转换是通过`舍弃小数`得到，而不是四舍五入 `(int)23.7 == 23; (int)-45.89f == -45`
- 强制类型转换
  - 条件是转换的数据类型必须是兼容的
  - 格式: (type)value
- 隐含强制类型转换
  - 整数的默认类型是 int
  - 浮点型不存在这种情况，因为在定义 float 类型时必须在数字后面跟上 F 或者 f

**Variable Types**
  - 局部变量
    > 访问修饰符不能用于局部变量
    > 局部变量是在`栈(后进先出)`上分配的
    > 没有默认值，所以被声明后，必须经过初始化才可以使用
  - 实例变量(全局变量)
    > 当对象被实例化之后，每个实例变量的值就跟着确定，在对象创建的时候创建，在对象被销毁的时候销毁
    > 访问修饰符可以修饰实例变量
    > 可以直接通过变量名访问，但在静态方法以及其他类中，就应该使用完全限定名：`ObejectReference.VariableName`
  - 类变量(静态变量)
    > 静态变量储存在静态存储区
    > 静态变量在第一次被访问时创建，在程序结束时销毁
    > 静态变量还可以在静态语句块中初始化
    > 静态变量可以通过：`ClassName.VariableName`的方式访问

**Modifier Types**
  - *访问修饰符*
    - `public`: 对所有类可见
      > main() 方法必须设置成公有的，否则，Java 解释器将不能运行该类
    - `protected`: 对同一包内的类和所有子类可见, 不能修饰类（外部类） [详解](https://www.runoob.com/w3cnote/java-protected-keyword-detailed-explanation.html)
      > `子类与基类在同一包中`：被声明为 protected 的变量、方法和构造器能被同一个包中的任何其他类访问；
      > `子类与基类不在同一包中`：在父类和子类不在同一个包中的前提下，对于子类来说，子类继承了父类所有的属性和方法（任何访问修饰符），虽然对从父类继承来的protected的属性和方法可见，但是只能在子类的内部进行访问，即：(this.)方法名、(this.)属性名进行访问和操作，而无法在外部对子类进行实例化，并用子类对象.protected方法或属性来访问。举个简单的例子，我们都知道Object类是所有类的父类，而在Object中有一个叫clone()的方法，那我们在实例化对象后能调用这个函数吗？通过实践证明是不可以的，给出的错误提示是：The method clone() from the type Object is not visible.该方法是不可见的，这就类似于我们刚刚提到的，虽然子类从父类中继承过来了包括protected的方法和属性，但对于外部的类（包括main函数中）都是无法获取到的。
    - `default`: (即默认，什么也不写）在同一包内可见
      > 接口里的变量都隐式声明为 public static final
      > 而接口里的方法默认情况下访问权限为 public
    - `private`: 仅在同一类内可见
      > 类和接口不能声明为 private
      > 主要用来隐藏类的实现细节和保护类的数据
    > *访问控制和继承*
    > 父类中声明为 public 的方法在子类中也必须为 public。
    > 父类中声明为 protected 的方法在子类中要么声明为 protected，要么声明为 public，不能声明为 private。
    > 父类中声明为 private 的方法，子类继承但子类没权限访问。
  - *非访问修饰符*
    - static
    - final
    - abstract
    - synchronized
  