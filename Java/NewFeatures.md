### Java 8
  - **Lambda 表达式**: 允许函数作为参数传递到方法中
    - 特征
      - 可选参数类型声明：不需要声明参数类型，编译器可以统一识别参数值
      - 可选的参数圆括号：一个参数无需定义圆括号，但多个和零个参数需要定义圆括号
      - 可选的大括号：如果主体包含了一个语句，就不需要使用大括号
      - 可选的返回关键字：如果主体只有一个表达式返回值则编译器会自动返回值, 大括号需要指明表达式返回了一个数值
      ``` Java
      // 1. 不需要参数,返回值为 5  
      () -> 5  
      // 2. 接收一个参数(数字类型),返回其2倍的值  
      x -> 2 * x  
      // 3. 接受2个参数(数字),并返回他们的差值  
      (x, y) -> x – y  
      // 4. 接收2个int型整数,返回他们的和  
      (int x, int y) -> x + y  
      // 5. 接受一个 string 对象,并在控制台打印,不返回任何值(看起来像是返回void)  
      (String s) -> System.out.print(s)

      Simple:
      public static void main(String[] args) {
          System.out.println(new Test1().operate(10, 5, (a, b) -> a + b));
      }

      @FunctionalInterface
      interface MathOperation {
          int operation(int x, int y);
      }

      private int operate(int a, int b, MathOperation mathOperation) {
          return mathOperation.operation(a, b);
      }
      ```
    - Lambda 表达式免去了使用匿名方法的麻烦，并且给予 Java 简单但是强大的函数化的编程能力
    - Lambda 表达式只能引用标记了 final 的外层局部变量，这就是说不能在 lambda 内部修改定义在域外的局部变量，否则会编译错误
    - Lambda 表达式的局部变量可以不用声明为 final，但是必须不可被后面的代码修改（即隐性的具有 final 的语义）
    - 当一个方法的参数是 Lambda 表达式时，这个参数类型一定是函数式接口
    
  - **方法引用**
    - 方法引用使用一对冒号 `::`, 通过方法的名字来指向一个方法, 可以使语言的构造更紧凑简洁, 减少冗余代码

    | 类型 | 语法 | 对应的Lambda表达式 |
    |  -- | -- | -- |
    | 静态方法引用 | 类名::staticMethod | (args) -> 类名.staticMethod(args) |
    | 实例方法引用 | inst::instMethod | (args) -> inst.instMethod(args) |
    | 对象方法引用 | 类名::instMethod | (inst,args) -> 类名.instMethod(args) |
    | 构建方法引用 | 类名::new | (args) -> new 类名(args) |

    - **对象方法引用**: 若 Lambda 参数列表中的第一个参数是实例方法的参数调用者，而第二个参数是实例方法的参数时，可以使用对象方法引用: 
      ``` Java 
        BiPredicate<String, String> bp = (x, y) -> x.equals(y);
        BiPredicate<String, String> bp1 = String::equals;

        System.out.println(bp1.test("xy", "xx"));
      ```

  - **函数式接口**: 有且仅有一个抽象方法，但可以有多个非抽象方法的接口

  - **默认方法**
    - 默认方法: `default resultType methodName(args...) { ... }`
    - 倘若一个类实现了多个接口，且这些接口有相同的默认方法：
      - 第一个解决方案是创建自己的默认方法，来覆盖重写接口的默认方法
        ``` Java
        public class Car implements Vehicle, FourWheeler {
          default void print(){
              System.out.println("我是一辆四轮汽车!");
          }
        }
        ```
      - 第二种解决方案可以使用 super 来调用指定接口的默认方法
        ``` Java
        public class Car implements Vehicle, FourWheeler {
          public void print(){
              Vehicle.super.print();
          }
        }
        ```
    - 静态默认方法: 接口可以声明（并且可以提供实现）静态方法 `static resultType methodName(args...) { ... }`

  - **Stream**
    - Stream 是一个来自数据源的元素队列并支持聚合操作
      - 数据源: 流的来源。 可以是集合，数组，I/O channel， 产生器generator 等
      - 聚合操作: 类似SQL语句一样的操作， 比如 filter, map, reduce, find, match, sorted 等
      - Pipelining: 中间操作都会返回流对象本身
      - 内部迭代
    - 生成流
      - stream() − 为集合创建串行流
      - parallelStream() − 为集合创建并行流
    - **forEach**: 迭代流中的每个数据
      > .forEach(System.out::println)
    - **map**: 用于映射每个元素到对应的结果
      > .map( i -> i * i)
    - **filter**: 用于通过设置的条件过滤出元素
      > .filter(string -> string.isEmpty())
    - **limit**: 用于获取指定数量的流
      > .limit(10)
    - **sorted**: 用于对流进行排序
      > .sorted()
    - **collect**: Collectors 类实现了很多归约操作，例如将流转换成集合和聚合元素。Collectors 可用于返回列表或字符串
      > .collect(Collectors.toList())  // to list
      > .collect(Collectors.joining(", ")) // 用 ', ' 连接list的元素并返回合并后的 string

  - **Optional Class**
    - Optional 类的引入很好的解决空指针异常 (`java.util.Optional<T>`)
    - 是一个可以为null的容器对象。如果值存在则 isPresent() 方法会返回 true，调用 get() 方法会返回该对象
    - 它可以保存类型T的值，或者仅仅保存null。Optional提供很多有用的方法，这样我们就不用显式进行空值检测

  - **Nashorn JavaScript**
    - 一个 javascript 引擎, 使用基于JSR 292的新语言特性, 其中包含在JDK 7中引入的 invokedynamic，将JavaScript编译成Java字节码
    - jjs: 是个基于Nashorn引擎的命令行工具。它接受一些JavaScript源代码为参数，并且执行这些源代码

- **Date Time API**
  - 本地化日期时间 API: LocalDate/LocalTime 和 LocalDateTime 类可以在处理时区不是必须的情况
    ``` Java
      LocalDateTime currentTime = LocalDateTime.now();
      LocalDate date1 = currentTime.toLocalDate();
    ```
  - 使用时区的日期时间API: ZonedDateTime
    ``` Java
      ZonedDateTime date1 = ZonedDateTime.parse("2015-12-03T10:15:30+05:30[Asia/Shanghai]");
      ZonedDateTime dateTime = ZonedDateTime.now();
      
      ZoneId zoneId = ZoneId.of("UTC+1");
      ZonedDateTime dateTime2 = ZonedDateTime.of(2015, 11, 30, 23, 45, 59, 1234, zoneId);
    ```

- **Base64**
  - Base64 工具类提供了一套静态方法获取下面三种 BASE64 编解码器:
    - **基本**：输出被映射到一组字符A-Za-z0-9+/，编码不添加任何行标，输出的解码仅支持A-Za-z0-9+/。
      - static Base64.Decoder getDecoder()
      - static Base64.Encoder getEncoder()
    - **URL**：输出映射到一组字符A-Za-z0-9+_，输出是URL和文件。
      - static Base64.Decoder getUrlDecoder()
      - static Base64.Encoder getUrlEncoder()
    - **MIME**：输出隐射到MIME友好格式。输出每行不超过76字符，并且使用'\r'并跟随'\n'作为分割。编码输出最后没有行分割。
      - static Base64.Decoder getMimeDecoder()
      - static Base64.Encoder getMimeEncoder()
      - static Base64.Encoder getMimeEncoder(int lineLength, byte[] lineSeparator) 可以通过参数指定每行的长度及行的分隔符
  ``` Java
    String base64Str = Base64.getEncoder().encodeToString(bytes); // 编码
    byte[] bytes = Base64.getDecoder().decode(base64Str); // 解码
  ```
