## 非线程安全Map

#### HashMap
* Map中键值K是唯一的，如果对同一个键值两次调用put方法，第二个加入的值V会覆盖第一个值。允许key和value为null。
* 如果HashMap太满 (当前load factor大于预设值) ，就需要对HashMap执行rehash操作。rehash的过程是创建一个新的HashMap，并将原Map中所有元素添加到新Map中，然后丢弃原Map。
* 要同时查看键与值，可以通过枚举各个条目 (Map.Entry) 查看，避免对值进行查找。
* 获取HashMap的大小不需要遍历Map。
##### JDK7实现
* HashMap采用位桶 (数组) 加链表实现。要查找表中元素的位置，先通过元素的hashcode方法计算出它的hashcode，然后与桶的总数取余，所得到的结果就是这个元素所在桶的索引 (hash算法) ，然后顺序遍历链表获取期望元素。
##### JDK8实现
* JDK8中HashMap被重新实现。采用位桶 (数组) 加链表或红黑树作为存储数据结构。如链表长度超过TREEIFY_THRESHOLD (8) 的值，则HashMap的数据将会从链表数组转化为树。即rehash时采用了不同与以往的方式进行rehash。
***

#### LinkedHashMap
##### JDK7
##### JDK8
* 使用一个双向链表存储Map中的Entry顺序关系，包括LRU顺序和插入顺序 (构造函数参数accessOrder的值，true表示访问顺序，false表示按插入顺序)。
* 通过覆写HashMap的newNode方法实现put元素时，创建扩展自HashMap.Node的LinkedHashMap.Entry。LinkedHashMap.Entry中存储了节点的hash值，key，value以及其前后节点的引用。
* LinkedHashMap同时持有头节点head和尾节点tail。
* LinkedHashMap可用来实现LRU缓存，但需要复写removeEldestEntry方法。定义在LinkedHashMap中的put或putAll方法会在加入新元素后调用afterNodeInsertion方法，而afterNodeInsertion方法会调用removeEldestEntry方法检查是否需要移除当前头结点。
***

#### WeakHashMap
只有当值 (value) 的生命周期是由该键 (key) 的外部引用而不是由值决定时，WeakHashMap才有用处。
1. 如果有一个值，对应的键已经不再使用。因为GC只跟踪活动的对象，只要Map是活动的，其中所有的桶也是活动的，那么它们就不能被回收。这种情况下使用WeakHashMap来完成回收。
2. 使用弱引用 (weak reference) 保存键。WeakReference对象将引用保存到另外一个对象 (散列表键) 中。对于这种类型的对象，GC使用一种特有的方式进行处理。
***

#### TreeMap
基于红黑树的可排序Map实现。
***

#### IdentityHashMap
* 键的hashcode不是由元素的hashcode函数计算，而是由System.identityHashCode方法计算。这是Object.hashCode方法根据对象的内存地址来计算散列码时所用的方式。
* 在两个对象比较时，IdentityHashMap使用==，而不是equals。
***

## 线程安全Map

#### ConcurrentHashMap
对检索完全同步，更新高预期同步的哈希表。减小了多线程下，更新操作和同步读取的竞争。
* 检索时未使用锁来实现同步，并且也不支持任何方式锁整个表来实现访问控制。
* 检索实现为非阻塞模式，仅保证弱一致性。
* 迭代器设计为每次仅能由一个线程使用。
* 组合操作如size方法，isEmpty方法和containsValue方法仅在没有其他线程更新当前表时有用 (弱一致性) 。
##### JDK7实现
* 通过定义继承自ReentrantLock的Segment类实现分段锁，默认分配16个锁。在每个桶上加上一个segment锁，实现并发访问时一个线程占用一把锁访问其中一段数据的时候，其他段上的数据仍能被其他线程访问。
* 仅在需要遍历整个map时才锁住所有桶。
##### JDK8实现
* 取消了Segment分段锁，采用CAS和synchronized关键字来保证并发安全。
* synchronized关键字只锁定当前链表或红黑树的首节点，这样只要hash不冲突，就不会产生竞争。
* 同样也是锁分离的思想，只是把锁分的比Segment更细。首先使用无锁操作CAS插入头结点，如果插入失败，说明已经有别的线程插入头结点了。如果头结点已经存在，则通过synchronized关键字获取头结点，进行后续操作。
***

#### ConcurrentSkipListMap
同步的可排序map。
