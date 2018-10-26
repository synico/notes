### 多SSH账号管理
#### 使用ssh-keygen生成本地秘钥
```
ssh-keygen -t rsa -C "synico@qq.com"
ssh-keygen -t rsa -C "212706300" -f ~/scm/hc-apm/.ssh/id_rsa
```
#### 本地添加私钥
```
ssh-add ~/.ssh/id_rsa_ge
```
#### 将公钥传输到远程机器
```
ssh-copy-id -i ~/.ssh/id_rsa_ge root@120.132.8.142
```
#### 添加配置文件
```
touch ~/.ssh/config
```
文件内容
```
Host github
  HostName github.com
  User synico@qq.com
  IdentityFile ~/.ssh/id_rsa

Host ge
  HostName github.build.ge.com
  User 212706300
  IdentityFile ~/scm/hc-apm/.ssh/id_rsa
```
***
