## NPM

### 安装模块
npm的包安装分为本地安装 (local) 和全局安装 (global)
#### 本地安装
将安装包放在./node_modules下 (运行npm命令时所在的目录) ，可以通过require()来引入本地安装的包。
```
npm install express
npm install express@4.17.1 // 安装模块特定版本
npm install --save (-S) express // 安装模块到项目node_modules目录下，并将模块依赖写入dependencies节点
npm install --save-dev (-D) gulp // 安装模块到项目node_modules目录下，并将模块依赖写入devDependencies节点
npm install --no-optional // 安装模块并忽略可选依赖

```
#### 全局安装
将安装包放在/usr/local下或者node的安装目录lib/node_modules下，可以直接在命令行使用。
```
npm install express -g
```
#### 查看安装信息
```
npm root -g   // 查看全局安装模块路径
npm list -g   // 查看全局安装模块
npm list  // 查看本地安装模块
npm list typescript -g // 查看全局模块中安装的typescript信息
npm view webpack version // 查看webpack在npm仓库上最新的可用版本
npm view webpack versions // 查看webpack在npm仓库上所有版本
```
#### 卸载模块
```
npm uninstall express
npm uninstall -S <package-name>
npm uninstall -D <package-name>
```
#### 更新模块
```
npm update express
```

***

### 换源
#### 临时替换
```
npm --registry https://registry.npm.taobao.org install express
```
#### 永久替换
```
npm config set registry https://registry.npm.taobao.org
```
#### 查看
```
npm config get registry
npm config list
```

***

### 代理
#### 设置代理
```
npm config set proxy http://server:port
npm config set https-proxy http://server:port
```
#### 设置代理用户名密码
```
npm config set proxy http://username:password@server:port
npm config set https-proxy http://username:password@server:port
```
#### 删除代理
```
npm config delete proxy
npm config delete https-proxy
```

***

### module.exports与exports
|module.exports|exports
：--|:--|:--
返回值|模块对象本身 (类)，需要new对象以后使用|模块函数，可直接使用

#### module.exports
#### exports
