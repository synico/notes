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
* 查看外部服务器
```
\des
```
* 枚举模式 (schema)
```
\dnS
```
```
SELECT * FROM PG_NAMESPACE;
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

### 创建用户并授权
* 使用超级用户登陆数据库，然后创建用户
```
CREATE USER testUser WITH PASSWORD '1qazxsw2';
```
* 将数据库权限授予testUser，但此时用户还是没有读写权限
```
GRANT ALL PRIVILEGES ON DATABASE testDB to testUser;
```
* 授予用户表权限
```
GRANT ALL PRIVILEGES ON all tables in schema public TO testUser; // 该SQL必须在所要操作的数据库里执行
GRANT SELECT ON TABLE mytable TO testUser;
```
***

### SQL命令
* 修改数据库名称
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
* 修改表名称
```
ALTER TABLE my_table_latest RENAME TO my_table;
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
* 查看库或表大小
```
SELECT pg_size_pretty(pg_database_size(my_database));
SELECT pg_size_pretty(pg_table_size(my_table));
```
***
