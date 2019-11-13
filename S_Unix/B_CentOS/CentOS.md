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

#### CentOS6查看开启端口
使用命令netstat

参数|含义
:--|:--
-a : all|表示列出所有的连接，服务监听，Socket资料
-t : tcp|列出tcp协议的服务
-u : udp|列出udp协议的服务
-n : port number|用端口号来显示
-l : listening|列出当前监听服务
-p : program|列出服务程序的PID

```
netstat -ntlp
```

***

### yum命令
命令|功能
:--|:--
search|查找软件包
list|列出所有可安装的软件包
list updates|列出所有可更新的软件包
list installed|列出所有已安装的软件包
list extras|列出所有已安装但不在Yum Repository内的软件包
info|列出所有软件包的信息
info updates|列出所有可更新的软件包信息
install file.rpm|安装rpm包，同时安装对应依赖包

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

### 安装网络工具
#### 查找软件
```
yum search [software_name]
yum search all [software_name]
```
#### 安装net-tools
```
yum install net-tools.x86_64
```
#### 安装openssh
```
yum install openssh*
```

### virtualbox安装centos7
#### 开启有线网络连接
默认情况下centos7 minimal不会开始有线网络连接，需要修改/etc/sysconfig/network-scripts下网卡对应的配置文件。
```
[root@localhost network-scripts]# ifconfig
enp0s3: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.0.2.15  netmask 255.255.255.0  broadcast 10.0.2.255
        inet6 fe80::d056:251a:327a:388f  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:54:49:c6  txqueuelen 1000  (Ethernet)
        RX packets 12  bytes 2350 (2.2 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 34  bytes 3109 (3.0 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

enp0s8: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.56.101  netmask 255.255.255.0  broadcast 192.168.56.255
        inet6 fe80::7597:612:8a07:5e04  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:22:12:80  txqueuelen 1000  (Ethernet)
        RX packets 145  bytes 18210 (17.7 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 98  bytes 15536 (15.1 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 8  bytes 656 (656.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 8  bytes 656 (656.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

其中网卡enp0s8对应的配置文件为:ifcfg-enp0s8
[root@localhost network-scripts]# cat ifcfg-enp0s8
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=dhcp
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=enp0s8
UUID=93cd5347-8d31-49ae-88e2-e6c7b397b410
DEVICE=enp0s8
ONBOOT=yes
其中ONBOOT默认值为no，需要将其由no改为yes。然后通过service network restart重启网络使配置生效。
```
