## Restful

### 版本控制
#### 无版本控制
无版本即平台强制使用一个API版本，不考虑兼容性。
#### URI中显示添加版本号
```
dev.github.com/v3/media/1
dev.github.com/media/1?v=3.0
```
* Pros: 直观，可直接看到API版本
* Cons: 违背了REST的HATEOAS (hypermedia as the engine of application state) 规则，版本号和资源之间并无直接关系。

#### 添加头信息控制版本
```
Accept: application/json;version=v2
```
* Pros: 遵循REST的HATEOAS原则
* Cons: 不够直观
