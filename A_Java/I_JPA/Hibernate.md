## Hibernate

### 实体状态 (EntityState)
#### 外部
##### EntityState.PERSISTENT
可能是刚保存的，或刚被加载的，它存在相关的Session作用范围内。Hibernate会检测到处于持久状态的对象的任何改动，在当前操作单元执行完毕时将对象数据与数据库同步，无需手动执行UPDATE。
##### EntityState.TRANSIENT
创建Hibernate Session后，由new操作符创建，且尚未与Session关联的对象。
##### EntityState.DETACHED
托管态，也叫游离态，与持久对象关联的Session被关闭后，对象就变为托管的。托管态不能直接持久化，需要重新保存。
##### EntityState.DELETED
调用Session的delete方法后，对象就变为删除态。此时Session中任然保留有对象的信息，对删除对象的引用依然有效，对象可继续被修改。删除态对象如果重新关联到某个新的Session，即执行持久化操作，会再次转化为持久态。

#### 内部
* Status.MANAGED
* Status.READ_ONLY
* Status.DELETED
* Status.GONE
* Status.LOADING
* Status.SAVING

#### 检查实体状态

***
