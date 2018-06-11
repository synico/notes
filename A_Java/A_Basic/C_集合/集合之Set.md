## 集合之Set

#### HashSet
1. HashSet由链表数组实现。使用HashMap作为存储载体。
2. 当不关心集合中元素顺序的时候才应该使用。

#### TreeSet
1. TreeSet是一个有序集合（Sorted Collection）。使用TreeMap作为存储载体。
2. 将一个元素添加到TreeSet中要比添加到HashSet中要慢，但是比将元素添加到数组或链表的指定位置要快。
3. 实现集合中元素按顺序排列的两种方法。第一，元素实现Comparable接口的compareTo方法。第二，将Comparator对象传递给TreeSet的构造器。

#### LinkedHashSet
此实现与HashSet的不同之处在于，其维护着一个运行于所有元素的双向链表。这个链表定义了遍历顺序，即按照元素插入到Set中的顺序进行遍历迭代。

#### CopyOnWriteArraySet
线程安全的Set实现，内部数据结构使用CopyOnWriteArrayList的Set。
1. 每次对Set的写入操作都复制产生新的数组，同CopyOnWriteArrayList。
2. 不支持在迭代器上使用remove方法。
3. 通过迭代器遍历速度快，并且不会与其他线程产生冲突。

#### ConcurrentSkipListSet
线程安全的可排序Set实现，基于ConcurrentSkipListMap的Set。
1. 不允许讲null加入该Set。
2. 其size方法需要遍历Set中所有元素，时间复杂度取决于Set大小。
3. 批量操作addAll，removeAll，retainAll和containsAll不保证以原子方式执行。
