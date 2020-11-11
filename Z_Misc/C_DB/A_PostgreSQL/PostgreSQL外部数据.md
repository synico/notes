## 外部数据 (Foreign Data)

### 安装插件依赖包
Postgresql默认仅安装server后，需要另外安装postgresql-contrib包后才能使用外部数据插件。
#### 在线安装
```
yum install -y postgresql-contrib
```

#### 离线安装
```
rpm -ivh libxslt-1.1.28-5.el7.x86_64.rpm --force --nodeps

rpm -ivh postgresql11-contrib-11.7-1PGDG.rhel7.x86_64.rpm
```

***

### postgres_fdw (Foreign Data Wrapper)
所有操作应切换至目标本地数据库。
#### 安装插件
```
CREATE EXTENSION postgres_fdw;
```

#### Foreign Server
* 创建Foreign Server

```
CREATE SERVER remote_server FOREIGN DATA WRAPPER postgres_fdw
  OPTIONS (host 'postgres.examp.com', port '5432', dbname 'remote_db');
```

* 查看已创建Foreign Server

```
postgres=#\des
```
```
postgres=# SELECT * FROM pg_foreign_server;
```

* 删除Foreign Server

```
DROP SERVER remote_server;
```

* 修改Foreign Server

```
ALTER SERVER remote_server OPTIONS (host 'pg.examp.com', db_name 'remote_db');
```

#### User Mapping
* 创建User Mapping

```
CREATE USER MAPPING FOR postgres SERVER remote_server
  OPTIONS (user 'postgres', password 'GehcDi9it@l');
```

* 查看已创建User Mapping

```
SELECT * FROM pg_user_mappings;
```

* 删除User Mapping

```
DROP USER MAPPING FOR postgres SERVER remote_server;
```

* 修改User Mapping

```
ALTER USER MAPPING FOR postgres SERVER remote_server
  OPTIONS (user 'postgres', password 'root');
```

#### 导入外部服务器SCHEMA

```
IMPORT FOREIGN SCHEMA remote_schema
  FROM SERVER remote_server INTO local_schema;

IMPORT FOREIGN SCHEMA remote_schema<public> LIMIT TO (remote_table<user_account>)
  FROM SERVER remote_server INTO local_schema;
```

#### 创建外部表Foreign Table

```
CREATE FOREIGN TABLE remote_table (login_name varchar(255), password varchar(255))
  SERVER remote_server OPTIONS (table_name 'user_account');
```

***

### dblink
#### 安装插件
```
CREATE EXTENSION dblink;
```
