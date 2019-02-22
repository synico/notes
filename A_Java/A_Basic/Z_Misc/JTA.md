## JPA (Java Transaction API)

### 实现原理
分布式事务 (Distributed Transaction) 包括事务管理器 (Transaction Manager) 和一个或多个支持XA协议的资源管理器 (Resource Manager)。

#### 事务管理器
* 负责所有事务参与单元的协调与控制。
* 面向开发人员的使用接口 (UserTransaction)，通过此接口实现分布式事务。

#### 资源管理器
* 任意类型的持久化数据存储。
* 面向服务提供商的实现接口，用来规范提供商 (如数据库连接提供商) 所提供的事务服务，它约定了事务的资源管理功能，使得JTA可以在异构事务资源之间执行协同。
***

### 体系结构
#### UserTransaction
#### Transaction
* 代表了一个物理意义上的事务，在调用UserTransaction.begin()方法时TransactionManager会创建一个Transaction事务对象 (标志事务的开始) 并把此对象通过ThreadLocal关联到当前线程。
* UserTransaction接口中的commit()，rollback()，getStatus()等方法都将最终委托给Transaction类的对应方法执行。

#### TransactionManager
本身并不承担实际的事务处理功能，更多的是充当用户接口和实现接口之间的桥梁。
***

### XA接口
#### XADataSource
支持事务的数据源与普通的数据源是不同的，它实现了额外的XADataSource接口。
#### XAConnection
由XADataSource返回的数据库连接与普通连接也是不同的，XAConnection额外增加了对分布式事务的支持。
***
