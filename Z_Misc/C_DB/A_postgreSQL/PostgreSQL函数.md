## PostgreSQL函数

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

### UUID函数
默认安装的Postgres是不带UUID函数，需要手动安装
```
create extension "uuid-ossp";
select uuid_generate_v4();
```
***
