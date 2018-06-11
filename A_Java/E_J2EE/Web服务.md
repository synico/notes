## Web服务

### JAX发展路径
JAX-RPC 1.0 -> JAX-RPC 1.1 -> JAX-WS (JAX-RPC 2.0)

### SOAP
SOAP = RPC + HTTP + XML

### JAXB (Java Architecture for XML Binding)
是一项业界标准，是JDK的组成部分，是一项可以根据XML Schema生成Java类的技术。该过程中JAXB提供了将XML实例文档反向生成Java类的方法，并能将Java对象树的内容重新写到XML实例文档。从另外一方面讲，JAXB提供了将XML绑定到Java。

### RESTful与Servlet的区别
#### Servlet是Java服务端的一种技术
* 核心理念是servlet与handler之间的一个mapping，利用配置文件来处理servlet和handler之间的mapping关系。
* servlet具有session状态，这方便服务器端实现一些带状态的逻辑。但同时也导致了servlet实现多服务器的架构带来了困难，就必须实现复杂的负载均衡，session复制，持久化机制。
* servlet获取客户端信息的方式更多的是通过request parameters。

#### RESTful是一个软件架构风格
* 通过请求URL来获取信息，路径即是信息。
* 无状态，状态通过应用层或数据层来维护。
* 通过HTTP的GET, POST, DELETE, PUT等方式来实现数据的CRUD。
