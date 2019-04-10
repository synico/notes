## SpringBoot

### 核心配置文件
在SpringBoot中有两种上下文，一种是bootstrap，另外一种是application。
#### bootstrap ( .yml或 .properties)
* bootstrap是应用程序的父上下文，即bootstrap加载优先于application。
* bootstrap主要用于从额外的资源来加载配置信息，还可以在本地外部配置文件中解密属性。
* bootstrap中属性不能被本地相同配置覆盖。
* 使用Spring Cloud Config配置中心时，需要在bootstrap配置文件中添加连接到配置中心的配置属性来加载外部配置中心的配置信息。

#### application ( .yml或 .properties)
主要用于SpringBoot项目的自动化配置。
***

### 开启SpringBoot的两种方式
#### 继承spring-boot-starter-parent
```
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.1.0.RELEASE</version>
</parent>
```
#### 引入spring-boot-dependencies依赖
```
<dependencyManagement>
    <dependencies>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-dependencies</artifactId>
        <version>2.1.0.RELEASE</version>
        <type>pom</type>
        <scope>import</scope>
    </dependencies>
</dependencyManagement>
```
***

### 核心注解
#### @Configuration
```
org.springframework.context.annotation.Configuration
```
用来代替applicationContext.xml配置文件，所有这个配置文件里能做到的事都可以通过这个注解所在类进行注册。
#### @ComponentScan
```
org.springframework.context.annotation.ComponentScan
```
用来代替配置文件中<component-scan/>配置，开启组件扫描，即自动扫描包路径下的@Component注解进行注册bean实例到spring容器的上下文里。而且该注解可重复使用，即可以配置多个，用来配置注册不同的子包。
#### @EnableAutoConfiguration
```
org.springframework.boot.autoconfigure.EnableAutoConfiguration
```
用来提供自动配置。
***

### 自动配置原理
#### 加载spring.factories
通过`org.springframework.core.io.support.SpringFactoriesLoader`加载classpath中的所有`META-INF/spring.factories`文件。
#### 初始化AutoConfiguration实例
初始化spring-boot-autoconfigure-version.jar的`META-INF/spring.factories`文件中定义的配置。即初始化如`DataSourceAutoConfiguration`。
```
# Auto Configure
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
org.springframework.boot.autoconfigure.admin.SpringApplicationAdminJmxAutoConfiguration,\
org.springframework.boot.autoconfigure.aop.AopAutoConfiguration,\
...
org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration,\
org.springframework.boot.autoconfigure.jdbc.JdbcTemplateAutoConfiguration,\
org.springframework.boot.autoconfigure.jdbc.JndiDataSourceAutoConfiguration,\
org.springframework.boot.autoconfigure.jdbc.XADataSourceAutoConfiguration,\
...
```
#### 查看自动配置报告
* spring-boot:run运行的对话框Enviroment中加入debug=true变量。
* java -jar xxx.jar --debug
* main方法运行，在VM arguments加入-Ddebug。
* 在application文件中加入debug=true。
* 如集成了spring-boot-starter-actuator，通过autoconfig端点可以直接查看。
***
