# 注解Annotation

#### 元注解
负责注解其他注解，Java5定义了4个标准的meta-annotation，用来提供对其他annotation类型做说明。

##### @Target 说明了注解所修饰对象的作用范围， 其取值ElementType有：  
1. CONSTRUCTOR：用于描述构造器  
2. FIELD：用于描述域  
3. LOCAL_VARIABLE：用于描述局部变量  
4. METHOD：用于描述方法  
5. PACKAGE：用于表述包  
6. PARAMETER：用于描述参数  
7. TYPE：用于描述类，接口，注解类型和enum声明

##### @Retention 说明了注解的生命周期，其取值RetentionPolicy有：  
1. SOURCE：在源文件中有效  
2. CLASS：在class文件中有效  
3. RUNTIME：在运行时有效

##### @Documented 用于描述其他类型注解应该被作为被标注的程序成员的公共API。是一个标记注解，没有成员（取值）

##### @Inherited 说明某个被标注的类型是被继承，是一个标记注解

#### 普通注解
1. 注解不能被继承，即父类上的注解不会自动被子类继承。
