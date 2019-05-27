## PostgreSQL命令

### 常用命令
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
***

### 运行sql脚本
```
psql -h localhost -U postgres -f createdb.sql
```
***

### 备份数据库
* 备份全库
```
pg_dump -h db_ip -U postgres db_name > dump.file
```
* 备份单表
```
pg_dump -h db_ip -U db_account -t table_name db_name > dump.sql
```
***

### 恢复数据库
* 恢复全库
```
psql -h db_ip -U postgres -d db_name < dump.file
```
* 恢复单表
```
psql -h db_ip -U db_account -d db_name < dump.sql
```
***

### SQL命令
* 修改数据库
```
ALTER DATABASE name RENAME TO new_name;
ALTER DATABASE name OWNER TO new_owner;
```
* 删除数据库
```
DROP DATABASE [IF EXISTS] name;
```
