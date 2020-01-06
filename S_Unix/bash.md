## Bash Shell

### 环境配置文件

#### 登录脚本 (login shell)
取得bash时需要完整登录流程的shell。由tty1-tty6登录，需要输入用户名密码，此时取得的bash就称为login shell。

读取顺序|文件名称|备注
:--|:--|:--
1.0|/etc/profile|系统整体配置文件
2.1|~/.bash_profile|如存在，则不继续读取2.2
2.2|~/.bash_login|如存在，则不继续读取2.3
2.3|~/.profile|

#### 非登录脚本 (non-login shell)
取得bash接口的方法不需要重复登录。由X-Window (tty7) 登录Linux以后，再以X的图形界面启动terminal，此时那个终端接口并没有需要再次输入账号和密码，那个bash的环境就称为non-login shell。non-login shell仅会读取~/.bashrc。

***

### 数据流重定向

#### 标准输入输出

流向|含义|示例
:--|:--|:--
标准输入 (stdin) |代码为0|<或<<
标准输出 (stdout) |代码为1|>或>>或1>或1>>
标准错误输出 (stderr) |代码为2|2>或2>>

#### /dev/null
/dev/null被称为黑洞设备，所有导向这个设备的信息都会被丢弃掉。
```
find /home -name .bashrc 2> /dev/null
```

#### 特殊写法
将正确与错误数据都写入一个文件，需要使用特殊写法保证写入顺序。
```
find /home -name .bashrc > list.txt 2>&1
find /home -name .bashrc &> list.txt
```

***
