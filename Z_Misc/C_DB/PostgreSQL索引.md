## PostgreSQL索引

### B-Tree
适合处理能够按顺序存储的数据之上的等于和范围查询，特别是在一个建立了索引的字段涉及到使用下列操作符进行比较的时候，PostgreSQL的查询规划器会考虑使用B-tree索引。
* <
* <=
* =
* \>=
* \>
* BETWEEN
* IN
* IS NULL
* IS NOT NULL
* LIKE和~，仅当模式是常量，并且昴定在字符串开头的时候，即col LIKE 'foo%'或col ~ '^foo'
***

### Hash
只能用于处理简单的等于比较。即当一个索引的列涉及使用=操作符进行比较的时候，查询规划器会考虑使用Hash索引。
***

### GIN (Generalized Inverted Index)
***

### GiST (Generalized Search Tree)
***

### SP-GiST (Space-Partitioned GiST)
***
