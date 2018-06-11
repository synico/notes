### Atom插件

#### 命令方式
Atom的插件实际上是在npm上，npm的官方源在国内访问是非常缓慢的。但是国内有许多镜像源可以使用，如淘宝源。可使用下面命令设置apm的更新源。

`apm config set registry https://registry.npm.taobao.org/`

`apm config set registry http://r.cnpmjs.org/`

#### 修改文件
直接修改.atom目录下.apmrc文件。
```
registry=https://registry.npm.taobao.org/
strict-ssl=false
```
