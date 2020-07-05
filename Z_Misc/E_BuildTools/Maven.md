## Maven

### Maven属性

#### 内置属性
主要有两个常用内置属性。
* `${basedir}`表示项目根目录，即包含pom.xml文件的目录
* `${version}`表示项目版本

#### POM属性
用户可以使用该类属性引用POM文件中对应元素的值。例如`${project.artifactId}`就对应了`<project> <artifactId>`元素的值。

属性名|对应值
:--|:--
`${project.groupId}`|项目的groupId
`${project.artifactId}`|项目的artifactId
`${project.version}`|项目的version，与`${version}`等价
`${project.outputDirectory}`|项目主代码编译输出目录，默认为target/classes/
`${project.testOutputDirectory}`|项目测试代码编译输出目录，默认为target/test-classes/
`${project.build.sourceDirectory}`|项目的主源码目录，默认为src/main/java/
`${project.build.testSourceDirectory}`|项目的测试源码目录，默认为src/test/java/
`${project.build.directory}`|项目构建输出目录，默认为target/
`${project.build.finalName}`|项目打包输出文件的名称，默认为`${project.artifactId}-${project.version}`

#### 自定义属性
用户可以在POM的`<properties>`元素下自定义Maven属性。

#### Settings属性
与POM属性同理，用户使用以`settings.`开头的属性应用settings.xml文件中XML元素的值，如常用的`${settings.localRepository}`指向用户本地仓库的地址。

#### Java系统属性
所有Java系统属性都可以使用Maven属性引用，例如`${user.home}`指向用户目录。可使用`mvn help:system`查看所有的Java系统属性。

#### 环境变量属性
所有环境变量都可以使用以`env.`开头的Maven属性引用。例如`${env.JAVA_HOME}`指代了JAVA_HOME环境变量的值。

***
