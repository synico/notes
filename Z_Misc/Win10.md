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
