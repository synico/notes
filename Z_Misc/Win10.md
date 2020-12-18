## Win10

### 配置WinHTTP代理
打开管理员命令提示符窗口，键入netsh，然后键入winhttp
#### set proxy
配置代理设置，可在命令后加上`/?`来查看此命令语法。
#### import proxy
导入Internet Explorer使用的代理信息。
```
import proxy source=ie
```
#### reset proxy
将WinHTTP代理重置为DIRECT。
#### show proxy
显示当前配置。

***

### Windows Terminal安装PowerLine
通过PowerShell的Install-Module命令安装Posh-Git和Oh-My-Posh
#### 安装Posh-Git
将Git状态信息添加到提示，并为Git命令，参数，远程和分支名称添加tab自动补全。
```
Install-Module posh-git -Scope CurrentUser
```
#### 安装Oh-My-Posh
为PowerShell提示符提供主题功能。
```
Install-Module oh-my-posh -Scope CurrentUser
```
#### 设置主题
```
Set-Theme Agnoster
```
#### 保存配置
在Windows Terminal下输入notepad $PROFILE打开配置文件。
```
Import-Module posh-git
Import-Module oh-my-posh
Set-Theme Agnoster

Set-ExecutionPolicy RemoteSigned //如果启动后报错
```

***
