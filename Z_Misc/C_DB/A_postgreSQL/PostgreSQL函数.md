## PostgreSQL函数

### 格式化函数
函数|返回类型|描述|例子
:--|:--|:--|:--
to_char(timestamp, text)|text|把时间戳转成字符串|to_char(current_timestamp, 'HH12:MI:SS')
to_char(interval, text)|text|把间隔转成字符串|to_char(interval '15h 2m 12s', 'HH24:MI:SS')
to_char(int, text)|text|把整数转成字符串|to_char(125, '999')
to_char(double precision, text)|text|把实数或双精度转成字符串|to_char(125.8::real, '999D9')
to_char(numeric, text)|text|把数字转成字符串|to_char(-128.8, '999D99S')
to_date(text, text)|date|把字符串转成数字|to_number('12,454.8-', '99G999D9S')
to_timestamp(text, text)|timestamp with time zone|把字符串转成时间戳|to_timestamp('05 Dec 2000', 'DD Mon YYYY')
***

### 数字转字符串
#### 函数to_char(int, text)
int为要转换的值，text为数值格式化模式参数

模式|描述
:--|:--
9|带有指定数值位数的值
0|带有前导0的值
.|小数点
,|分组 (千) 分隔符

#### 操作符||
通过操作符||连接数字和''
```
select 12345||''
```
***

### 字符串转数字
#### 函数to_number(text1, text2)
text1为要转的数字字符串，text2为数值格式化模式参数
#### 函数cast(text as int/integer)
```
select cast('12345' as integer)
select cast('12345' as int)
```
#### 操作符::
```
select '12345'::int
```
***

### COALESCE函数
函数返回参数中的第一非null的值，要求参数中至少有一个是非null的，如果参数都是null会报错
```
select COALESCE(null,null); //报错
select COALESCE(null, null, now()::varchar, ''); //结果会得到当前时间
select COALESCE(null, null, '', now()::varchar); //结果会得到''
```
***

### UUID函数
默认安装的Postgres是不带UUID函数，需要手动安装
```
create extension "uuid-ossp";
select uuid_generate_v4();
```
***
