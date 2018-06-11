## 集合之List

### ArrayList
数据结构：由数组实现，可随机访问 (实现了RandomAccess接口) 。  
遍历：可以通过数组下标遍历访问列表中元素。或通过实现Iterator接口的Itr来遍历，其最终也是通过数组下标访问列表中元素。所以用下标和Iterator遍历ArrayList效率相差不大。  
Add：调用add方法向列表添加元素时，如果添加位置在数组末尾，不需要复制移动数组。如果add时指定了加入位置，则调用System.arraycopy()来复制移动数组其他元素，效率较低。  
Remove：调用remove方法删除列表中元素时，如果根据元素在列表中位置 (数组下标) 来删除，仅需要复制移动数组剩余元素。如果通过对象引用来删除该对象，需要先遍历数组来确定该对象位置，然后根据其位置来删除，并复制移动数组剩余元素。  
元素类型：可以添加null到列表。  

1. 除了实现List接口，还实现了RandomAccess接口。
2. 两个ArrayList equals表示两个ArrayList含有相同的元素，并且元素的顺序相同。
3. 在ArrayList的末尾添加删除元素效率高。基于效率的考虑，避免使用contains， index，remove(Object)，removeAll和retainAll。
4. ArrayList仅有trimToSize方法可以压缩它的容量，而clear或remove*方法只能改变其长度。
***

### LinkedList
数据结构：由双向链表实现，是有序列表。  
遍历：如果通过index访问遍历链表中元素，每次都会循环遍历链表，效率很差。而通过Iterator (ListIterator) 遍历，效率会高。  
Add：将元素添加到任何位置都不需要移动链表中其他元素。如果添加元素到指定位置，则需要遍历指定位置之前所有元素。但是添加到列表尾则不需要遍历任何元素。添加一个元素到列表，将创建4个对象(1. node本身 2. previous pointer 3. next pointer 4. 元素的值) 。  
Remove：调用remove方法移除链表中元素，仅需遍历链表找到要移出元素位置，不需要复制移动链表其他元素。  
元素类型：可以添加null到链表。  

1. 使用LinkedList的唯一原因是需要在列表中间频繁添加删除元素。
2. 不要使用LinkedList中任何接受或返回元素位置 (index) 的方法。
3. 除了实现List接口，还实现了Deque接口。如要实现FIFO，使用ArrayDeque是更好的选择。
4. 两个LinkedList equals表示两个LinkedList含有相同的元素，并且元素的顺序相同。
***

### 数组和链表
* 数组中的数据在内存中顺序存放，插入，删除数据时需要移动其他数据项。要访问数组中元素可通过下标index快速访问。
* 链表中的数据在内存中随机存放，可以适应数据动态的增减，可方便的插入，删除数据项。如果要访问链表中的指定元素，需要从链表的头逐个遍历，直到找到所需要的元素为止。
* 使用链表的唯一理由是尽可能地减少在列表中间插入或删除元素所付出的代价。
* 避免使用以整数索引表示链表中位置的所有方法。如果需要对列表进行随机访问，就使用数组或ArrayList，而不要使用LinkedList。
* 可以将任意类型的数据加入到列表，包括null和基本类型。
* 使用Iterator遍历List同时要remove/add修改List时，需要用Iterator的remove/add方法，而不是List的reomve/add方法。如果使用List的remove/add方法会导致ConcurrentModificationException。
***

### CopyOnWriteArrayList
List的同步版本，通过每次写入 (包括add，set和remove操作) 时复制对象数组 (存储数据结构) 实现线程安全。简单说只要正确发布一个事实不变的对象，那么在访问该对象时就不需要进一步同步。而在每次修改List时，都创建并重新发布一个新的容器副本，从而实现写时可变性。迭代器仅保证弱一致性。
* 在需要线程安全时，遍历读取操作的数量大大超过写操作数量时，这种非阻塞的线程安全实现可能比其他方案更有效。
* 不支持在其迭代器上对元素进行更改操作（remove, set和add），否则抛出UnsupportedOperationException。
* 对列表读实现为非阻塞，但对列表的写入以阻塞的方式实现。写入时使用ReentrantLock保证线程安全。

用途：可用在事件通知系统，在分发通知时需要迭代已注册监听器链表，并调用每一个监听器，在大多数情况下，注册和注销事件监听器的操作远少于接收事件通知的操作。
