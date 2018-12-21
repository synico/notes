## CentOS

### 防火墙
#### firewall-cmd
* 查看所有打开的端口
```
firewall-cmd --zone=public --list-ports
```
* 查看所有区域
```
firewall-cmd --list-all-zones
```
* 查看活动区域信息
```
firewall-cmd --get-active-zones
```
* 查看指定接口所属区域
```
firewall-cmd --get-zone-of-interface=eth0
```
* 拒绝所有包
```
firewall-cmd --panic-on
```
* 取消拒绝状态
```
firewall-cmd --panic-off
```
* 查看是否拒绝
```
firewall-cmd --query-panic
```
* 开启端口
```
firewall-cmd --zone=public --add-port=80/tcp --permanent
```
* 更新防火墙规则
```
firewall-cmd --reload
```
* 查看特定端口防火墙规则
```
firewall-cmd --zone=public --query-port=80/tcp
```
* 删除特定端口防火墙规则
```
firewall-cmd --zone=public --remove-port=80/tcp --permanent
```
