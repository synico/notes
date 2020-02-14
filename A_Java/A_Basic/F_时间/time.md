## java.time

java.time中所有class都是不可变类，线程安全。

包|说明
:--|:--
java.time|基于ISO_8601日历系统实现的日期时间库
java.time.chrono|全球日历系统扩展库，可以自行扩展
java.time.format|日期时间格式，包含预定义的格式，可以自行扩展
java.time.zone|时区信息库
java.time.temporal|日期时间调整辅助库

***

### Date新增方法
```
// 从Date获取Instant
public Instant toInstant() {
  return Instant.ofEpochMilli(getTime());
}

// 从Instant获取Date
public static Date from(Instant instant) {
  try {
    return new Date(instant.toEpochMilli());
  } catch (ArithmeticException ex) {
    throw new IllegalArgumentException(ex);
  }
}
```
***

### Instant
代表时间戳。
***

### LocalDate
代表不包含具体的时间的年月日，比如yyyy-MM-dd。
***

### LocalTime
代表不含年月日，仅包含时间的日期，比如hh:mm:ss。
#### 字符串转LocalTime
```
DateTimeFormatter localTimeFormatter = DateTimeFormatter.ofPattern("HH:mm:ss");
LocalTime.parse("08:00:00", localTimeFormatter);
```
***

### LocalDateTime
代表包含年月日和时间的日期，但不包含偏移信息 (时区) 。
***

### ZonedDateTime
代表包含时区的完整日期，偏移量是以UTC/格林威治时间为基准。
***

### 日期格式化
#### DateTimeFormatter
