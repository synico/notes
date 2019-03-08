## CentOS

### 换源
#### 备份本地yum源
```
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.bak
```
#### 替换yum源文件
```
wget -O /etc/yum.repos.d/CentOS-Base.repo  http://mirrors.aliyun.com/repo/Centos-7.repo
```
#### 更新cache
```
yum makecache
```
#### 查看
```
yum -y update
```
***

### 防火墙
#### firewalld
/etc/firewalld/zones

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
***

### 安装使用docker
#### 通过rpm包安装docker
```
sudo yum install docker.rpm
```
#### 通过rpm包升级docker
```
sudo yum -y upgrade
```
#### 启动docker
```
sudo systemctl start docker
```
#### 设置开机启动
```
sudo systemctl enable docker
sudo systemctl disable docker
```
***

### 修改主机名
#### hostnamectl
通过hostnamectl命令修改主机名，立即生效并且重启也生效。
```
hostnamectl set-hostname nick.vbox.com
```
#### /etc/hosts
直接修改/etc/hosts文件，需要重启后生效
```
127.0.0.1         nick.vbox.com
或
192.168.56.103    nick.vbox.com
```
***
