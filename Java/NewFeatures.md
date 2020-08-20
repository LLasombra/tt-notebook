### Java 8
  - Lambda 表达式: 允许函数作为参数传递到方法中
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