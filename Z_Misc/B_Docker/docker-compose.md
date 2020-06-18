## docker-compose命令

### 参数
#### -f, --file FILE
指定除默认docker-compose.yml的其他文件作为启动配置文件。
```
docker-compose -f ~/data/dev/docker-compose-dev.yml
docker-compose --file ~/data/dev/docker-compose-dev.yml
```
#### -p, --project-name name
指定自选的项目名，而不使用默认值目录名为项目名。
```
docker-compose -p sit
docker-compose --project-name sit
```
***

### 命令
#### up
创建并运行容器
```
docker-compose -f ~/data/sit/docker-compose-sit.yml up
```
* -d, --detach
```
docker-compose -f ~/data/sit/docker-compose-sit.yml up -d
```

***

### 编排文件
#### 定义时区
* 方法一
```
environment:
  - SET_CONTAINER_TIMEZONE=true
  - CONTAINER_TIMEZONE=Asia/Shanghai
```
* 方法二
```
environment:
  - TZ=Asia/Shanghai
```
