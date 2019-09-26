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
pg_dump -h db_ip -U db_account -d db_name -t table_name > dump.sql
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
* 修改默认用户postgres密码
```
ALTER USER postgres WITH PASSWORD 'postgres';
```
* 表索引
```
SELECT * FROM pg_indexes WHERE schemaname='public';
SELECT * FROM pg_statio_all_indexes WHERE schemaname='public';
```
* 查看表
```
SELECT * FROM pg_tables WHERE schemaname='public';
```
* 查看视图
```
SELECT * FROM pg_views WHERE schemaname='public';
```
* 断开所有连接用户
```
SELECT pg_terminate_backend(pid) FROM pg_stat_activity WHERE datname='dbname' AND pid<>pg_backend_pid();
```
***
