## MySQL配置

### 打开binlog
先找到[mysqld]，增加log-bin和server-id配置。
#### log-bin
binlog文件前缀。
#### server-id
其值介于1到 (2<sup>32</sup>) -1，为该实例在replication group中的唯一标识。
```
[mysqld]
log-bin=mysql-bin
server-id=1
```
***
