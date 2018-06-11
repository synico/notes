## Spring事务隔离级别和传播级别

### 事务相关术语
#### Dirty reads (脏读)
事务T1修改了某数据但并未提交，事务T2读取该数据，然后T1撤销（rollback）对某数据的修改，则事务T2在T1回滚前读取到的数据是无效的脏数据。
#### Non-repeatable reads (不可重复读)
一个事务范围内两次相同的查询得到不同的数据。事务T1读取了某数据，然后事务T2修改并提交了该数据，当事务T1第二次读取该数据时，事务T1两次读取的数据不一致。针对T2的更新 (列) 操作。
#### Phantom reads (幻读)
事务T1读取与搜索条件匹配的若干行数据，事务T2以删除或插入等方式修改事务T1的结果集，并提交。当事务T1再次读取数据时，事务T1发现两次读取数据不一致。针对T2删除数条已有记录 (行) 或新插入数条 (行) 数据。
***

### 事务隔离级别
#### ISOLATION\_READ\_UNCOMMITTED
隔离的最低级别，可能出现dirty reads，non-repeatable reads和phantom reads。该级别的事务可以读取其他事务已修改但未提交的数据。
#### ISOLATION\_READ\_COMMITTED
该隔离级别的事务禁止读取其他事务修改但未提交的数据。可以避免dirty reads，但是仍不能避免non-repeatable reads和phantom reads。
#### ISOLATION\_REPEATABLE\_READ
可以避免dirty reads和non-repeatable reads，但是仍不能避免phantom reads。
#### ISOLATION\_SERIALIZABLE
事务隔离的最高级别，可以避免dirty reads，non-repeatable reads和phantom reads。
***

### 事务传播级别
#### PROPAGATION\_REQUIRED
Spring事务模型中事务传播的默认级别。当前上下文环境中已有事务，加入到上下文中已有事务中执行。如当前上下文环境中没有事务，则新建事务执行。
#### PROPAGATION\_SUPPORTS
当前上下文环境中已有事务，加入到当前事务中执行。如当前上下文环境中没有事务，则按非事务的方式执行。
#### PROPAGATION\_MANDATORY
当前上下文环境中已有事务，加入到当前事务中执行。如当前上下文环境中没有事务，则抛出异常。
#### PROPAGATION\_REQUIRES\_NEW
当前上下文环境中已有事务，先挂起已有事务，并创建新事务执行，待新建事务执行完毕后恢复执行已有事务。
#### PROPAGATION\_NOT\_SUPPORTED
当前上下文环境中已有事务，先挂起已有事务，以非事务的方式执行，待其执行完毕后恢复执行已有事务。
#### PROPAGATION\_NEVER
当前上下文环境中已有事务，则抛出异常。如没有事务，以非事务方式执行。
#### PROPAGATION\_NESTED
当前上下文环境中已有事务，则事务嵌套在已有事务中执行，作为已有事务的子事务执行。如上下文环境中没有事务，则新建事务执行。
