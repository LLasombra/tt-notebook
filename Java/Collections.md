### 集合框架
  - 是一个用来代表和操纵集合的统一架构, 集合框架都包含如下内容:
    - 接口: 是代表集合的抽象数据类型
      - Collection 接口存储一组不唯一，无序的对象
      - **List** 接口存储一组不唯一，有序（插入顺序）的对象。类似数组，可以动态增长。查找元素效率高，插入删除效率低，因为会引起其他元素位置改变
      - **Set** 接口存储一组唯一，无序的对象。检索效率低下，删除和插入效率高
      - SortedSet 继承于 Set 保存有序的集合
      - Map 接口存储一组键值对象
      - Map.Entry 描述在一个 Map 中的一个元素（键/值对）, 是一个 Map 的内部类
      - SortedMap 继承于 Map，使 Key 保持在升序排列
    - 实现（类）：是集合接口的具体实现
      - AbstractList
      - LinkedList 非同步，解决方法就是在创建List时候构造一个同步的List
        `List list = Collections.synchronizedList(newLinkedList(...));`
      - ArrayList 非同步
      - Vector 和 ArrayList 非常相似，同步
      - Stack 是 Vector 的一个子类，实现了一个标准的后进先出的栈
      - AbstractSet
      - HashSet
      - TreeSet
      - AbstractMap
      - HashMap 非同步
      - TreeMap
    - 算法：是实现集合接口的对象里的方法执行的一些有用的计算
      - Collection Algorithms 这里是一个列表中的所有算法实现
    ![](https://www.runoob.com/wp-content/uploads/2014/01/java-coll.png)
  - Java 集合框架主要包括两种类型的容器：
    - 集合（Collection），存储一个元素集合
    - 图（Map），存储键/值对映射
  - 位于java.util包
  - 遍历Map
    - 通过 **Map.keySet** 遍历key
    - 通过 **Map.entrySet** 使用iterator遍历, `Iterator<Map.Entry<String, String>> it = map.entrySet().iterator();`
    - 通过 **Map.entrySet** 遍历key和value, (推荐，尤其是容量大时) `Set<Map.Entry<String, String>> entryseSet = map.entrySet();`
    - 通过 **Map.values()** 遍历所有的value，但不能遍历key
    - 综合比较在只遍历 key 的时候使用 keySet(), 在只遍历 value 的是使用 values() 方法, 在遍历 key-value 的时候使用 entrySet() 是比较合理的选择
  - java.util 包下的集合类都是 **快速失败（fail—fast）** 的，不能在多线程下发生并发修改（迭代过程中被修改）
  - java.util.concurrent 包下的容器都是 **安全失败（fail—safe）**，可以在多线程下并发使用，并发修改
![集合框架图](https://www.runoob.com/wp-content/uploads/2014/01/2243690-9cd9c896e0d512ed.gif)