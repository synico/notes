## 集合之Queue
Queue|线程安全|有界
:--|:--|:--
PriorityQueue|不安全|无界
ArrayDeque|不安全|有界
LinkedList|不安全|无界
ConcurrentLinkedQueue|安全|无界
ConcurrentLinkedDeque|安全|无界
ArrayBlockingQueue|安全|有界
LinkedBlockingQueue|安全|无界
LinkedBlockingDeque|安全|无界
PriorityBlockingQueue|安全|
LinkedTransferQueue||
DelayQueue||
SynchronousQueue|安全|无容量
***

### Queue

Queue定义的方法

操作|抛出异常|返回特殊值
:--|:--|:--
插入|add(e)|offer(e)
移除|remove()|poll()
检查|element()|peek()
***

#### PriorityQueue
* 由高效的数据结构堆 (可自我调整的二叉树) 实现。  
* 不允许添加null到队列中，否则抛出NPE。  
* 元素按任意顺序插入，但总是按照排序的顺序检索。
* 既可以保存实现了Comparable接口的对象，也可以保存利用构造器提供Comparator的对象。
#### ConcurrentLinkedQueue
基于链接节点的线程安全但无阻塞的无限队列，按照先进先出FIFO对元素进行排序。入列时，元素插入到队列的尾部；出列时，从队列的头部获取元素。
* 其迭代器仅提供弱一致性，仅反映某一时刻或迭代器创建时队列的状态。
* 所有批处理操作如addAll方法，equals方法和toArray方法都不保证原子性。
* 通过sun.misc.Unsafe的Unsafe机制实现无阻塞的线程安全。
* size方法时间复杂度为O(n)，而不像一般的容器为O(1)。该方法会遍历Queue中所有元素。并且结果也不一定准确。
***

### Deque

Deque定义的方法
* 头元素

操作|抛出异常|返回特殊值
:--|:--|:--
插入|addFirst(e)|offerFirst(e)
移除|removeFirst()|pollFirst()
检查|getFirst()|peekFirst()

* 尾元素

操作|抛出异常|返回特殊值
:--|:--|:--
插入|addLast(e)|offerLast(e)
移除|removeLast()|pollLast()
检查|getLast()|peekLast()

* Queue和Deque方法比较

Queue方法|等价的Deque方法
:--|:--
add(e)|addLast(e)
offer(e)|offerLast(e)
remove()|removeFirst()
poll()|pollFirst()
element()|getFirst()
peek()|peekFirst()

* Stack和Deque方法比较

Stack方法|等价的Deque方法
:--|:--
push(e)|addFirst(e)
pop()|removeFirst()
peek()|peekFirst()
***

#### ArrayDeque
* 由循环数组实现，两个数组下标 (head, tail)保存数组头尾信息。数组头尾都可以添加删除元素，但是不能在队列中间添加元素。  
* 不允许添加null到队列中，否则抛出NPE。  
* 需要实现FILO时，ArrayDeque比使用Stack快。
* 需要实现FIFO时，ArrayDeque比使用LinkedList快。因为使用LinkedList，在向其中添加元素时，需要创建更多的对象来完成存储。在GC运行时，需要更多的时间回收更多的空间。
* 有界双端队列，最多扩容30次。
***

### BlockingQueue
#### BlockingQueue方法
BlockingQUeue的方法以四种形式出现，对于不能立即满足但可能在将来某一时刻可以满足的操作，这四种形式的处理方式不同。
* 第一种是抛出异常
* 第二种是返回一个特殊值 (null或布尔值，具体取决于操作)
* 第三种是在操作成功前，无限期的阻塞当前线程
* 第四种是在放弃前只在给定的最大时间限制内阻塞

操作|抛出异常|特殊值|阻塞|给定时间内阻塞
:--|:--|:--|:--|:--
插入|add(e)|offer(e)|put(e)|offer(e, time, unit)
移除|remove()|poll()|take()|poll(time, unit)
检查|element()|peek()|无|无
***

#### ArrayBlockingQueue
* 以数组作为存储结构的FIFO有界阻塞队列，使用ReentrantLock锁实现线程安全。
* 新加入的元素存于队列的尾部，从队列的头部检出元素。
* 队列的大小在创建时指定，之后无法更改。
* 试图将元素加入 (put方法) 已满的队列，或试图从空队列中检出 (take方法) 元素都会导致阻塞。
* 支持公平锁和非公平锁。

#### LinkedBlockingQueue
* 以链表作为存储结构的FIFO可选边界阻塞队列，使用ReentrantLock锁实现线程安全。
* 新加入的元素存于队列的尾部，从队列的头部检出元素。
* 队列的大小可在Queue创建时指定，也可以不指定 (无界队列) 。
* 如果是有界队列，试图将元素加入 (put方法) 已满的队列，或试图从空队列中检出 (take方法) 元素都会导致阻塞。
* 链表队列的吞吐量通常高于数组队列，但是在并发情况下，链表队列可预测的性能不如数组队列。

#### SynchronousQueue
* 容量为0的阻塞队列，每个插入动作都需要等待另外一个线程对应的移除动作，反之亦然。在没有显示同步的情况下，当两个线程准备好将一个对象从一个线程传递到另一个线程时使用。
* 不能调用peek方法检索队列中元素，总是返回null。因为仅当从队列移除某元素时，该元素才会出现在队列中。
* 公平策略，使用TransferQueue，等待的线程通过FIFO顺序竞争访问。非公平策略，使用TransferStack，等待的线程无序的竞争访问。

#### DelayQueue

#### PriorityBlockingQueue
* 头元素

操作|抛出异常|特殊值|阻塞|给定时间内阻塞
:--|:--|:--|:--|:--
插入|addFirst(e)|offerFirst(e)|putFirst(e)|offerFirst(e, time, unit)
移除|removeFirst()|pollFirst()|takeFirst()|pollFirst(time, unit)
检查|getFirst()|peekFirst()|无|无

* 尾元素

操作|抛出异常|特殊值|阻塞|给定时间内阻塞
:--|:--|:--|:--|:--
插入|addLast(e)|offerLast(e)|putLast(e)|offerLast(e, time, unit)
移除|removeLast()|pollLast()|takeLast()|pollLast(time, unit)
检查|getLast()|peekLast()|无|无
***

### BlockingDeque
#### BlockingDeque方法


***
#### ConcurrentLinkedDeque
#### LinkedBlockingDeque
LinkedBlockingDeque是可选容量的阻塞队列，如果没有设置容量，那么容量是Integer.MAX_VALUE。
