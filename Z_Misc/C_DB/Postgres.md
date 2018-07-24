### Postgres

#### 常用命令
* 连接数据库
```
psql -U username -h dbHost -p dbPort -d dbName
```
* 切换数据库
```
\c dbName
```
* 枚举数据库
```
\l
```
* 枚举表
```
\dt
```
* 查看表结构
```
\d tableName
```
* 查看索引
```
\di
```
* 退出psql
```
\q
```

#### 运行sql脚本
```
psql -h localhost -U postgres -f createdb.sql
```
