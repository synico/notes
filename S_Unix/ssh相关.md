### 多SSH账号管理
#### 使用ssh-keygen生成本地秘钥
* -t表示秘钥的格式
* -C表示秘钥的注释
* -f表示生成秘钥的文件名，包括路径
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

#### ssh相关问题
执行ssh-add报Could not open a connection to your authentication agent错误，通过执行`ssh-agent bash`即可解决。
