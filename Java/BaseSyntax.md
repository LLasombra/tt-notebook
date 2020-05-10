### Setup
  - [Download JDK](https://www.oracle.com/java/technologies/javase-downloads.html)
  - Config System Environment -> Run -> sysdm.cpl
      > 变量名：JAVA_HOME -> 变量值：C:\Program Files (x86)\Java\jdk1.8.0_91  //要根据自己的实际路径配置
      > 变量名：Path -> 变量值：%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;
      > 变量名：CLASSPATH -> 变量值：.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;  //记得前面有个".", JDK1.5以上可不设置也可以正常编译和运行 Java 程序
  - IDE Download
      > [Eclipse](http://www.eclipse.org/downloads/packages/)
      > [IntelliJ IDEA](https://www.jetbrains.com/idea/download/#section=windows)

### Coding Style
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

### Class And Object

### DataTypes
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

### Variable Types
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

### Modifier Types
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
    - static: 静态变量, 静态方法
    - final: 修饰的类不能被继承, 修饰的方法不能被子类重写, 修饰的变量为常量且不可修改
    - abstract: 
      - 抽象类
        > 抽象类不能用来实例化对象
        > 如果一个类包含抽象方法，那么该类一定要声明为抽象类
        > 抽象类可以包含抽象方法和非抽象方法
      - 抽象方法
        > 任何继承抽象类的子类必须实现父类的所有抽象方法，除非该子类也是抽象类
        > 抽象类可以不包含抽象方法
    - synchronized: 声明的方法同一时间只能被一个线程访问
    - transient: 序列化的对象包含被 transient 修饰的实例变量时, JVM会忽略transient变量的原始值并将默认值保存到文件中
    - volatile: 修饰的成员变量在每次被线程访问时, 都会强制从共享内存中重新读取该成员变量的值, 当变量改变时, 会强制线程将变化值回写到共享内存。这样在任何时刻, 两个不同的线程总是看到某个成员变量的同一个值。一个 volatile 对象引用可能是 null

### Java Operators  
- 算术运算符: +, -, *, /, &, %, ++, --
  - 前缀自增自减法(++a, --a): 先进行自增或者自减运算，再进行表达式运算
  - 后缀自增自减法(a++, a--): 先进行表达式运算，再进行自增或者自减运算
- 关系运算符: ==, !=, >, >=, <, <=
- 位运算符
  - `&  ` 与 相对应位都是 1，则结果为 1，否则为 0
  - `|  ` 或 相对应位都是 0，则结果为 0，否则为 1
  - `^  ` 异或 如果相对应位值相同，则结果为0，否则为1
  - `~  ` 按位取反运算符翻转操作数的每一位，即0变成1，1变成0
  - `<< ` 按位左移运算符。左操作数按位左移右操作数指定的位数
  - `>> ` 按位右移运算符。左操作数按位右移右操作数指定的位数
  - `>>>` 按位右移补零操作符。左操作数的值按右操作数指定的位数右移，移动得到的空位以零填充
- 逻辑运算符: &&, ||, !
- 赋值运算符: =, +=, -=, *=, /=, %=, <<=, >>=, >>>=, &=, ^=, |=
- 三目运算符: ? :
- 其他运算符: 
  - instanceof: 该运算符用于操作对象实例，检查该对象是否是一个特定类型(类或接口)
    ```
    String name = "James";
    boolean result = name instanceof String; // 由于 name 是 String 类型，所以返回真
    ```
    如果被比较的对象兼容于右侧类型,该运算符仍然返回true

### Loop
  - while(布尔表达式) {}
  - do {} while(布尔表达式)
  - for(初始化 ; 布尔表达式 ; 更新) {}
  - for(声明元素名 : 数组名或返回数组的方法名) {}
  > break, continue

### Condition
  - if() {}
  - if() {} else {}
  - if() {} else if() {} else {}
  - 嵌套

### Switch Case
  > 判断一个变量与一系列值中某个值是否相等，每个值称为一个分支
  ``` Java
    switch(expression) {
      case value :
        //语句
        break; //可选
      case value :
        //语句
        break; //可选
      //你可以有任意数量的case语句
      default : //可选
        //语句
    }
  ```
  - switch变量可以是: byte, short, int, char, String(JDK 7开始)。case标签必须为字符串常量或字面量, 且数据类型与变量的相同
  - default 分支不需要 break 语句, 可以在任何位置，但通常在最后一个
  - 如果匹配成功的 case 语句块中没有 break 语句, 从当前 case 开始, 后续所有 case 的值都会执行, 直到遇到break则跳出switch

### Number And Math
  - 所有基本数值类型的包装类(Integer、Long、Byte、Double、Float、Short)都是抽象类Number的子类
  - 装箱, 拆箱
  - Number & Math 类方法
    > xxxValue(): 用于将 Number 对象转换为 xxx 数据类型的值并返回
    > compareTo(): 方法用于将 Number 对象与方法的参数进行比较
    > equals(): 方法用于判断 Number 对象与方法的参数进是否相等
    > valueOf(): 方法用于返回给定参数的原生 Number 对象值，参数可以是原生数据类型, String等
    > abs(): 返回参数的绝对值
    > random(): 方法用于返回一个随机数，随机数范围为 0.0 =< Math.random < 1.0

### Character Class
  - 将一个char类型的参数传递给需要一个Character类型参数的方法时，那么编译器会自动地将char类型参数转换为Character对象。 这种特征称为装箱，反过来称为拆箱
  - Character 类方法
    > isLetter(): 方法用于判断指定字符是否为字母
    > isDigit(): 方法用于判断指定字符是否为数字
    > isUpperCase(), toUpperCase(): 是否是大写字母, 指定字母的大写形式
    > isLowerCase(), toLowerCase(): 是否是小写字母, 指定字母的小写形式

### String Class
  - 在 Java 中字符串属于对象，并提供了 String 类来创建和操作字符串
  - String 类的静态方法 format() 能用来创建可复用的格式化字符串
    ``` Java
    String fs;
    fs = String.format("浮点型变量的值为 " +
      "%f, 整型变量的值为 " +
      " %d, 字符串变量的值为 " +
      " %s", floatVar, intVar, stringVar);
    ```
  - String 类方法
    - length() 返回字符串对象包含的字符数
    - char charAt(int index)用于返回指定索引处(0 到 length() - 1)的字符
    - int compareTo(Object o), int compareTo(String anotherString), int compareToIgnoreCase(String str)
    - boolean equalsIgnoreCase(String anotherString) 将字符串与指定的对象比较，不考虑大小写
    - boolean endsWith(String suffix) 方法用于测试字符串是否以指定的后缀结束
      > startsWith()
    - int indexOf(int ch): 返回指定字符在字符串中第一次出现处的索引
    - int lastIndexOf(int ch): 返回指定字符在此字符串中最后一次出现处的索引
    - String replace(char oldChar, char newChar) 用 newChar 字符替换字符串中出现的所有 oldChar 字符，并返回替换后的新字符串
    - replaceAll(), replaceFirst()
    - String[] split() 方法根据匹配给定的正则表达式来拆分字符串
      > `. $ | * `等转义字符，必须得加 `\\`
      > 多个分隔符，可以用` | `作为连字符
    - substring() 方法返回字符串的子字符串
    - toUpperCase() 方法将字符串小写字符转换为大写, toLowerCase() 方法将字符串转换为小写
    - trim() 方法用于删除字符串的头尾空白符

### StringBuffer & StringBuilder
  - 与String相比, StringBuffer和StringBuilder类的对象能够被多次的修改，并且不产生新的未使用对象
  - StringBuilder: 线程不安全, 但性能更好, 单线程中使用, 常用
  - StringBuffer: 线程安全(方法都使用了synchronized), 多线程中使用
  - 主要方法:
    - append(String s) 将指定的字符串追加到此字符序列
    - reverse() 字符序列反转
    - replace(int start, int end, String str) 使用给定 str 中的字符替换此序列start - end的的字符

### Array
  - 用来存储固定大小的同类型元素
    ``` Java
    dataType[] arrayRefVar = new dataType[arraySize];
    dataType[] arrayRefVar = {value0, value1, ..., valuen};

    int[] a = new int[10];
    ```
  - 数组的元素是通过索引访问的, 索引值从 0 到 arrayRefVar.length - 1
  - 多维数组 可以看成是数组的数组, 比如二维数组就是一个特殊的一维数组, 其每一个元素都是一个一维数组
    ``` Java
    type[][] typeName = new type[typeLength1][typeLength2];
    String[][] str = new String[3][4];

    String[][] s = new String[2][];
    s[0] = new String[2];
    s[1] = new String[3];
    s[0][0] = new String("Good");
    s[0][1] = new String("Luck");
    s[1][0] = new String("to");
    s[1][1] = new String("you");
    s[1][2] = new String("!");
    ```
  - java.util.Arrays 类能方便地操作数组，它提供的所有方法都是静态的
    - void sort(Object[] a): 升序排列
    - int binarySearch(Object[] a, Object key): 对排序好的数组进行二分查找法操作

### DateTime
  - **java.util.Date** 类方法:
    - boolean after(Date date), boolean before(Date date): 调用此方法的Date对象在指定日期之后/之前返回true
    - int compareTo(Date date), boolean equals(Object date): 比较当调用此方法的Date对象和指定日期
    - long getTime(): 返回时间戳, void setTime(long time)毫秒数设置时间和日期
  - **SimpleDateFormat** 选择任何用户自定义日期格式化
    ``` Java
    SimpleDateFormat ft = new SimpleDateFormat("MMM d, yyyy-MM-dd HH:mm:ss:SSS", Locale.ENGLISH);
    System.out.println(ft.format(new Date()));

    SimpleDateFormat ft2 = new SimpleDateFormat("yyyy-MM-dd");
    System.out.println(ft.format(ft2.parse("1818-11-11")));
    ```
    - 有的格式分大小写, 如 MM 是月份，mm 是分；HH 是 24 小时制，而 hh 是 12 小时制, ss 秒, SSS 毫秒
    - parse() 解析字符串为时间
  - **printf**格式化日期
    - 以 %t 开头并且以(c 包括全部日期和时间信息, F, D, r, T, R)中的一个字母结尾
  - sleep(): 使当前线程进入停滞状态(阻塞当前线程), 让出CPU的使用、目的是不让当前线程独自霸占该进程所获的CPU资源，以留一定时间给其他线程执行的机会, `Thread.sleep(1000 * 3);  // 休眠3秒`
  - 测量时间: System.currentTimeMillis() 之差
  - **Calendar** 抽象类: 设置和获取日期数据的特定部分, 公历日历
    - 创建Calendar对象:
      ``` Java
      Calendar c = Calendar.getInstance();  // c默认是当前日期
      c.set(2020, 4 - 1, 18);  // 创建一个代表2020年4月18日的Calendar对象
      ```
    - 对象信息的设置:
      - Set设置
        > 调用 public final void set(int year,int month,int date)
        > 如果只设定某个字段，例如年份的值: public void set(int field, int value)
        > c.set(Calendar.YEAR, 2008)
      - Add设置
        > c对象的日期减去10，也就是c表示为10天前的日期
        > c.add(Calendar.DATE, -10);
    - Calender的月份是从0开始的，但日期和年份是从1开始的
  - **GregorianCalendar** 类是Calendar抽象类的一个具体实现
    - Calendar.getInstance()返回一个默认用当前的语言环境和时区初始化的GregorianCalendar对象
    - 构造方法如: 
      ``` Java
      GregorianCalendar()
      GregorianCalendar(int year, int month, int date)
      GregorianCalendar(TimeZone zone)
      ```
    - 常用方法如: 
      ``` Java
      void add(int field, int amount)  // 根据日历规则，将指定的（有符号的）时间量添加到给定的日历字段中
      int get(int field)  // 获取指定字段的时间值
      Date getTime()  // 获取日历当前时间
      TimeZone getTimeZone()  // 获取时区
      boolean isLeapYear(int year)  // 确定给定的年份是否为闰年
      void set(int field, int value)  // 用给定的值设置时间字段
      void set(int year, int month, int date)  // 设置年、月、日的值
      void setTime(Date date)
      void setTimeInMillis(long millis)
      void setTimeZone(TimeZone value)
      ```
    ``` Java
    GregorianCalendar gcalendar = new GregorianCalendar();
    gcalendar.get(Calendar.MONTH);
    ```

### Regular Expression
  - 定义了字符串的模式, 可以用来搜索、编辑或处理文本, 并不仅限于某一种语言，但是在每种语言中有细微的差别
  - java.util.regex 包主要包括以下三个类:
    - Pattern 类: 是一个正则表达式的编译表示, 没有公共构造方法
    - Matcher 类: 是对输入字符串进行解释和匹配操作的引擎, 没有公共构造方法
    - PatternSyntaxException 类: 非强制异常类，它表示一个正则表达式模式中的语法错误
      - public String getDescription() 获取错误的描述
      - public int getIndex() 获取错误的索引
      - public String getPattern() 获取错误的正则表达式模式
      - public String getMessage() 返回多行字符串，包含语法错误及其索引的描述、错误的正则表达式模式和模式中错误索引的可视化指示
    ``` Java
      // 按指定模式在字符串查找
      String line = "This order was placed for QT3000! OK?";
      String pattern = "(\\D*)(\\d+)(.*)";
      // 创建 Pattern 对象
      Pattern r = Pattern.compile(pattern);
      // 现在创建 matcher 对象
      Matcher m = r.matcher(line);
      if (m.find()) {
         System.out.println("Found value: " + m.group(0) );
         System.out.println("Found value: " + m.group(1) );
         System.out.println("Found value: " + m.group(2) );
         System.out.println("Found value: " + m.group(3) ); 
      } else {
         System.out.println("NO MATCH");
      }

      Found value: This order was placed for QT3000! OK?
      Found value: This order was placed for QT
      Found value: 3000
      Found value: ! OK?
    ```
  - 捕获组: 把多个字符当一个单独单元进行处理的方法，它通过对括号内的字符分组来创建
    - 如: `((A)(B(C)))` 有 `((A)(B(C))), (A), (B(C)), (C)` 四个组
    - 可以通过调用 matcher 对象的 groupCount 方法来查看表达式有多少个分组
  - 正则表达式语法
    - Java 中，`\\` 表示：我要插入一个正则表达式的反斜线，所以其后的字符具有特殊的意义, 所以表示一位数字的正则表达式是 `\\d`, 而表示一个普通的反斜杠是 `\\\\`
    - 字符说明:
      - `\`: 将下一字符标记为特殊字符、文本、反向引用或八进制转义符
      - `x|y`: 匹配 x 或 y, 如`z|food` 匹配"z"或"food"。`(z|f)ood` 匹配"zood"或"food"
      - `^`: 匹配输入字符串开始的位置, `$`: 结尾的位置
      - `.`: 匹配除"\r\n"之外的任何单个字符
      - `*`: 零次或多次匹配前面的字符或子表达式, `+`: 一次或多次 `等效于 {1,}`,  `?`: 零次或一次 `等效于 {0, 1}`
      - `{n}`: n 是非负整数。正好匹配 n 次, `{n,}`: 至少匹配 n 次 ,`{n, m}`: 匹配至少 n 次，至多 m 次
      - `[xyz]`: 字符集, `[^xyz]`: 反向字符集, 如 "[abc]"匹配"plain"中的"a", "[^abc]"匹配"plain"中"p"，"l"，"i"，"n"
      - `[a-z]`: 字符范围, `[^a-z]`: 反向范围字符
      - `\b`: 匹配一个字边界, `\B`: 非字边界匹配, 如 "er\b"匹配"never"中的"er"，但不匹配"verb"中的"er"
      - `\d`: 数字字符匹配, 等效于 [0-9], `\D`: 非数字字符匹配, 等效于 [^0-9]
      - `\w`: 匹配任何字类字符, 包括下划线, 与"[A-Za-z0-9_]"等效, `\W`: 与任何非单词字符匹配
      - `(pattern)`: 匹配 pattern 并捕获该匹配的子表达式, 如 `(\\d(\\d))\\2`, `\\2`代表引用前面的第2组匹配的值, "211"
      - `(?:pattern)`: 匹配 pattern 但不捕获该匹配的子表达式，即它是一个非捕获匹配，不存储供以后使用的匹配, 如 `industr(?:y|ies)` 是比 `industry|industries` 更经济的表达式
      - `(?=pattern)`: 非捕获匹配, 如 `Windows (?=95|98|NT|2000)` 匹配"Windows 2000"中的"Windows", 但不匹配"Windows 3.1"中的"Windows"
      - `(?!pattern)`: 非捕获匹配, 如 `Windows (?!95|98|NT|2000)` 匹配"Windows 3.1"中的 "Windows"，但不匹配"Windows 2000"中的"Windows"
      - [更多](https://www.runoob.com/java/java-regular-expressions.html)
  - Matcher 类的方法
    - 索引方法
      - public int start() 返回以前匹配的初始索引
      - public int end() 返回最后匹配字符之后的偏移量
      - [例子](https://www.runoob.com/java/java-regular-expressions.html)
    - 研究方法
    - 替换方法
      - replaceFirst 替换首次匹配，replaceAll 替换所有匹配
      ``` Java
        private static String REGEX = "dog";
        private static String INPUT = "The dog says meow. " + "All dogs say meow.";
        private static String REPLACE = "cat";

        public static void main(String[] args) {
          Pattern p = Pattern.compile(REGEX);
          // get a matcher object
          Matcher m = p.matcher(INPUT); 
          INPUT = m.replaceAll(REPLACE);
          System.out.println(INPUT);
        }

        The cat says meow. All cats say meow.
      ```

### Java Method
  - 方法是解决一类问题的步骤的有序组合, 能使程序变得更简短而清晰, 有利于程序维护, 可以提高程序开发的效率和代码重用性
  - 命名规则: 
    - 第一个单词以小写字母开头, 后面单词则用大写字母开头, 不使用连接符
    - 下划线可能出现在 JUnit 测试方法名称中用以分隔名称的逻辑组件。一个典型的模式是: `test<MethodUnderTest>_<state>`, 例如 `testPop_emptyStack`
  - 方法包含一个方法头和一个方法体
    ![方法结构](https://www.runoob.com/wp-content/uploads/2013/12/12-130Q1220955916.jpg)
  - 参数列表: 是指方法的参数类型、顺序和参数的个数
  - `方法签名`: 方法名和参数列表
  - 方法调用:
    - 当方法返回一个值的时候, 方法调用通常被当做一个值, 如: `int larger = max(30, 40);`
    - 当方法返回值是void, 方法调用一定是一条语句
  - 命令行参数: 是在执行程序时候紧跟在程序名字后面的信息, main(String args[])
    ``` Java
      $ javac CommandLine.java 
      $ java CommandLine this is a command line 200 -100
    ```
  - 可变参数: 在方法声明中，在指定参数类型后加一个省略号: `...`
    > 一个方法中只能指定一个可变参数，它必须是方法的最后一个参数, 编译器会将其转型为一个数组, 可向函数传递 0 个或多个参数
    void function(String... args);
    void function(String [] args);
    这两个方法的命名是相等的，不能作为方法的重载

    > 对于可变参数的方法重载: 
    void function(String... args);
    void function(String args1,String args2);
    function("Wallen","John");
    优先匹配固定参数的方法
  - finalize() 方法: 在对象被垃圾收集器析构(回收)之前调用, 用来清除回收对象
    ``` Java
      public class Test1 {
          public static void main(String[] args) {
              Cake c1 = new Cake(1);
              Cake c2 = new Cake(2);
              Cake c3 = new Cake(3);
              c2 = c3 = null;
              System.gc(); // 调用Java垃圾收集器
          }
      }

      class Cake {
          private int id;

          public Cake(int id) {
              this.id = id;
              System.out.println("Cake Object" + id + " is created");
          }

          @Override
          protected void finalize() throws java.lang.Throwable {
              super.finalize();
              System.out.println("Cake Object" + id + " is disposed");
          }
      }

      Cake Object1 is created
      Cake Object2 is created
      Cake Object3 is created
      Cake Object2 is disposed
      Cake Object3 is disposed
    ```

### Files IO
  - Stream: 一个流可以理解为一个数据序列。输入流表示从一个源读取数据，输出流表示向一个目标写数据
  - 读取控制台输入: System.in
    - 获得一个绑定到控制台的字符流, `BufferedReader br = new BufferedReader(new InputStreamReader(System.in));`
    - `read()` 方法从控制台读取一个字符, `readLine()` 方法读取一个字符串
      ``` Java
        // 使用 System.in 创建 BufferedReader
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str;
        System.out.println("Enter 'end' to quit.");
        do {
          str = br.readLine();
          System.out.println(str);
        } while (!str.equals("end"));
      ```
  - 控制台输出
    - 控制台的输出由 print() 和 println() 完成, 由类 PrintStream 定义, System.out 是该类对象的一个引用
  - 读写文件
    - FileInputStream
      - 使用**字符串类型**的文件名来创建一个输入流对象来读取文件: `InputStream fis = new FileInputStream("C:/java/hello");`
      - 使用一个**文件对象**来创建: `InputStream fis2 = new FileInputStream(new File("C:/java/hello"));`
    - FileOutputStream
      - 使用**字符串类型**的文件名来创建一个输出流对象
      - 使用一个**文件对象**来创建
  - InputStreamWriter, OutputStreamWriter对象, 参数可以指定编码
  - Java中的目录
    - 创建目录
      - mkdir()  方法创建一个文件夹
      - mkdirs() 方法创建一个文件夹和它的所有父文件夹
    - 读取目录
      - 一个目录其实就是一个 File 对象, 它包含其他文件和文件夹
      - 如果创建一个 File 对象并且它是一个目录, 那么调用 `isDirectory()` 方法会返回 true,  `String[] list()` 方法可提取它包含的文件和文件夹的列表, `File[] listFiles()` 用 File 对象形式返回目录下的指定类型的所有文件和文件夹
    - 删除目录或文件
      - java.io.File.delete() 方法删除文件
      - 删除某一目录时, 必须保证该目录下没有其他文件才能正确删除
        ``` Java
          public static void main(String args[]) {
              File folder = new File("/tmp/java/");  // 测试的目录
              deleteFolder(folder);
          }
      
          // 删除文件及目录
          public static void deleteFolder(File folder) {
              File[] files = folder.listFiles();
              if (files != null) {
                  for (File f : files) {
                      if (f.isDirectory()) {
                          deleteFolder(f);
                      } else {
                          f.delete();
                      }
                  }
              }
              folder.delete();
          }
        ```

  ![IO流的类层次图](https://www.runoob.com/wp-content/uploads/2013/12/iostream2xx.png)
  
### Scanner Class
  - java.util.Scanner 是 Java5 的新特征, 可以获取用户的输入, `Scanner s = new Scanner(System.in);`
  - 通过 Scanner 类的 `next()` 与 `nextLine()` 方法获取输入的字符串，在读取前我们一般需要 使用 `hasNext` 与 `hasNextLine` 判断是否还有输入的数据
  - next() 与 nextLine() 区别: 
    - next(): 一定要读取到有效字符后才可以结束输入, 只有输入有效字符后才将其后面输入的空白作为分隔符或者结束符, 不能得到带有空格的字符串, 即遇到空格结束, 去除首空格
    - nextLine(): 以Enter为结束符, 可以获得空白, 返回的是输入回车之前的所有字符
  - 也支持输入 int 或 float 类型的数据, `hasNextXxx()`, `nextXxx()`
    - 如: hasNextFloat(), nextFloat()
  -  scan.close(); 记得关流

### Exception
  - 三种类型的异常: 
    - **检查性异常(编译时异常)**: Exception类中除了 RuntimeException 类及其子类都是编译时异常, 特点是Java编译器会对其进行检查，如果出现异常就必须对异常进行处理，否则程序无法通过编译
      - 使用try…catch语句对异常进行捕获
      - 使用throws关键字声明抛出异常，调用者对其处理
    - **运行时异常**: RuntimeException 类及其子类都是运行时异常, 特点是Java编译器不会对其进行检查, 一般是由程序中的逻辑错误引起的, 如数组角标越界
    - **错误**: 不是异常, 而是脱离程序员控制的问题, 用来指示运行时环境发生的错误, 如OutOfMemoryError。异常能被程序本身处理, 错误是无法处理
  - Exception 类的层次
    ![Exception class hierarchy](https://www.runoob.com/wp-content/uploads/2017/09/690102-20160728164909622-1770558953.png)
  - 捕获异常
    - try/catch 代码块中的代码称为保护代码, catch 语句包含要捕获异常类型的声明
    - 当保护代码块中发生一个异常时，try 后面的 catch 块就会被检查, 如果发生的异常包含在 catch 块中，异常会被传递到该 catch 块
    - **多重捕获**: 一个 try 代码块后面跟随多个 catch 代码块。如果多个 catch 块中的异常出现继承关系，父类异常 catch 块放在最下面
    - catch 里处理异常的时候不要简单的e.printStackTrace(), 而是应该进行详细的处理, 如进行 `console 打印详情`或者进行`日志记录`
  - throws/throw 关键字
    - 如果一个方法没有捕获到一个检查性异常, 那么该方法必须使用 throws 关键字来声明, 放在方法签名的尾部
    - 也可以使用 throw 关键字抛出一个异常，无论它是新实例化的还是刚捕获到的
  - finally 关键字
    - 用来创建在 try 代码块后面执行的代码块, finally 代码块出现在 catch 代码块最后
    - 无论是否发生异常，finally 代码块中的代码总会被执行
    - finally 并非一定被执行, 如果 catch 块中有退出系统的语句 System.exit(-1); finally就不会被执行
    - finally 永远都会在 catch 的 return 前被执行
      ``` Java
        try{
          //待捕获代码    
        }catch（Exception e）{
            System.out.println("catch is begin");
            return 1 ;
        }finally{
            System.out.println("finally is begin");
            return 2 ;
        }

        catch is begin
        finally is begin 
        return 2
      ```
  - 自定义异常
    - 所有异常都必须是 Throwable 的子类: 
      - 如果希望写一个`检查性异常类`，则需要继承 `Exception` 类
      - 如果你想写一个`运行时异常类`，那么需要继承 `RuntimeException` 类
  - Java中定义了两种类型的异常和错误
    - **JVM(Java虚拟机) 异常**：由 JVM 抛出的异常或错误, 如NullPointerException 类, ClassCastException 类
    - **程序级异常**：由程序或者API程序抛出的异常, 如 IllegalArgumentException 类, IllegalStateException 类

### Extends/Implements
  - 继承特性 : 
    - 单继承, 多实现
    - 子类拥有父类非 private 的属性、方法
    - 子类可以重写父类的方法
    - 提高类之间的耦合性(继承的缺点, 耦合度高就会造成代码之间的联系越紧密, 代码独立性越差)
  - extends: 子类单继承父类
  - implements: 类可以实现多个接口
  - this: 指向当前对象, super: 指向当前对象的父类
  - 如果父类只有有参构造器，则必须在子类的构造器中显式地通过 super 关键字调用父类的有参构造器
  - 如果父类有无参构造器，则在子类的构造器中系统会自动调用父类的无参构造器
  - 转型: 父类引用指向子类对象
    ``` Java
      Father f1 = new Son();   // 这就叫 upcasting （向上转型)
      // 现在 f1 引用指向一个Son对象

      Son s1 = (Son)f1;   // 这就叫 downcasting (向下转型)
      // 现在f1 还是指向 Son对象

      Father f2 = new Father();
      Son s2 = (Son)f2;       // 出错，子类引用不能指向父类对象
    ```
    - 父类引用指向子类对象，而子类引用不能指向父类对象
    - 把子类对象直接赋给父类引用叫**向上转型**(upcasting)，向上转型不用强制转换
    - 把指向子类对象的父类引用赋给子类引用叫**向下转型**(downcasting)，要强制转换

### Override/Overload
  - 重写
    - 重写是在子类存在方法与父类的方法的名字相同,而且参数的个数与类型一样,返回值也一样的方法,就称为重写
    - 重写规则
      - 重写方法不能抛出新的检查异常或者比被重写方法声明更加广泛的检查异常
      - 返回类型与被重写方法的返回类型可以不相同，但是必须是父类返回值的派生类(jdk7+)
      - 访问权限不能比父类中被重写的方法的访问权限更低
  - 重载
    - 重载是一个类中定义了多个方法名相同,而他们的参数的数量不同或数量相同而类型和次序不同,则称为方法的重载。返回类型可以相同也可以不同
    - 重载规则
      - 被重载的方法可以改变返回类型
      - 被重载的方法可以改变访问修饰符
      - 被重载的方法可以声明新的或更广泛的检查异常
  - 方法的重写和重载是java多态性的不同表现，重写是子父类之间多态性的一种表现，重载是一个类的多态性表现

### polymorphism
  - 多态是同一个行为具有多个不同表现形式或形态的能力
  - 优点: 
    1. 消除类型之间的耦合关系
    2. 可替换性
    3. 可扩充性
    4. 接口性
    5. 灵活性
    6. 简化性
  - 多态存在的三个必要条件: 
    - 继承
    - 重写
    - 父类引用指向子类对象
  - 当使用多态方式调用方法时，首先检查父类中是否有该方法，如果没有，则编译错误；如果有，再去调用子类的同名方法
  - 子类的同名静态成员方法会被父类的同名静态成员方法隐藏，也就是说被父类的静态方法覆盖
  - 多态的实现方式: 
    - 重写
    - 接口
    - 抽象类和抽象方法

### Abstract Class
  - 