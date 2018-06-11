# Replication和Shard

#### 1. Replicaiton
复制生成的索引，利用round-robin（轮询调度）来实现性能提升。

#### 2. Shards
当出现内存不足或索引太大时，可将索引拆分成多个部分（每个部分称为Shard），并部署在不同的物理机上。

#### 3. Solr Cloud
Sharding和Replication

#### 4. Core
多个core可实现在一个单独的solr实例中创建不同的配置和不同的索引结构。
