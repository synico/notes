## nodejs

### npm换源
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

### npm代理
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
