## JDK8新特性

### 函数式接口
***

### Lambda表达式
Lambda表达式可以引用类成员和局部变量，但会将这些变量隐式的转换为final变量。
***

### 接口的增强
***

### 集合之流式操作
***

### 注解的更新
#### 类型注解 (Type Annotation)
在定义注解类型的ElementType里增加了TYPE_PARAMETER和TYPE_USE两种新的类型。
* ElementType.TYPE_PARAMETER表示这个注解可用在Type的声明式前。
* ElementType.TYPE_USE表示这个注解可用在所有使用Type的地方，如泛型，类型转换等。
#### 重复注解 (Repeating Annotation)
在需要对同一个声明式或者类型加上相同的注解 (包含不同的属性值) 的情况，使用@Repeatable注解声明Container Annotation来存储重复的注解。
***

### 安全性
***

### 全球化功能
***

### IO/NIO的改进
***

### 时间类
JDK8中的时间类都是线程安全的不可变类型
#### Instant代替Date
#### LocalDateTime代替Calendar
#### DateTimeFormatter代替SimpleDateFormat

#### java.time
主要提供dates，times，instants和durations的API。
* Instant - a timestamp, is the closest equivalent class to java.util.Date
* LocalDate - a date without a time, or any reference to an offset or time-zone
* LocalTime - a time without a date, or any reference to an offset or time-zone
* LocalDateTime - combines date and time, but still without any offset or time-zone
* ZonedDateTime - a full date-time with time-zone and resolved offset from UTC/Greenwich, is the closest equivalent class to java.util.GregorianCalendar
* Duration - a time-based amount of time
* Period - a date-based amount of time

#### java.time.chrono
#### java.time.format
#### java.time.temporal
#### java.time.zone
***
