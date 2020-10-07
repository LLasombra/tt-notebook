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

### ArrayList
  - ArrayList 类继承了 AbstractList，并实现了 List 接口。是一个可以动态修改的数组，与普通数组的区别就是它是没有固定大小的限制，我们可以添加或删除元素
  - `ArrayList<E>` E 只能为引用数据类型
![ArrayList](https://www.runoob.com/wp-content/uploads/2020/06/ArrayList-1-768x406-1.png)

### LinkedList
  - 链表（Linked list）是一种常见的基础数据结构，是一种线性表，但是并不会按线性的顺序存储数据，而是在每一个节点里存到下一个节点的地址。可分单向链表和双向链表
    - 一个单向链表包含两个值: 当前节点的值和一个指向下一个节点的链接
    - 一个双向链表有三个整数值: 数值、向后的节点链接、向前的节点链接
  - LinkedList（链表） 类似于 ArrayList，是一种常用的数据容器。与 ArrayList 相比，LinkedList 的增加和删除对操作效率更高，而查找和修改的操作效率较低
  - 更多的情况下我们使用 ArrayList 访问列表中的随机元素更加高效，但以下几种情况 LinkedList 提供了更高效的方法
    - 使用 addFirst() 在头部添加元素
    - 使用 addLast() 在尾部添加元素
    - 使用 removeFirst() 移除头部元素
    - 使用 removeLast() 移除尾部元素
    - 使用 getFirst() 获取头部元素
    - 使用 getLast() 获取尾部元素
![LinkedList](https://www.runoob.com/wp-content/uploads/2020/06/20190328164737.png)

### HashSet
  - HashSet 基于 HashMap 来实现的，是一个不允许有重复元素的集合，是无序的，即不会记录插入的顺序
  - 不是线程安全的， 如果多个线程尝试同时修改 HashSet，则最终结果是不确定的。必须在多线程访问时显式同步对 HashSet 的并发访问
  - 允许有 null 值
![HashSet](https://www.runoob.com/wp-content/uploads/2020/07/java-hashset-hierarchy.png)

### HashMap
  - HashMap 是一个散列表，它存储的内容是键值对(key-value)映射
  - HashMap 实现了 Map 接口，根据键的 HashCode 值存储数据，具有很快的访问速度，最多允许一条记录的键为 null，不支持线程同步
  - HashMap 是无序的，即不会记录插入的顺序。继承于AbstractMap，实现了 Map、Cloneable、java.io.Serializable 接口
![HashMap](https://www.runoob.com/wp-content/uploads/2020/07/WV9wXLl.png)

### Iterator
  - Iterator（迭代器）不是一个集合，它是一种用于访问集合的方法，可用于迭代 ArrayList 和 HashSet 等集合
    - 获取迭代器 `Iterator<String> it = list.iterator();`
    - 调用 it.hasNext() 用于检测集合中是否还有元素。
    - 调用 it.next() 会返回迭代器的下一个元素，并且更新迭代器的状态。
    - 调用 it.remove() 将迭代器返回的元素删除。
    ``` Java
    // 让迭代器 it 逐个返回集合中所有元素最简单的方法是使用 while 循环：
    while(it.hasNext()) {
        System.out.println(it.next());
    }
    ```
