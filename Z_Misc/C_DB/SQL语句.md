## SQL语句

### WHERE与HAVING的区别
#### WHERE
WHERE是一个约束声明，使用WHERE来约束来自数据库的数据，WHERE是在结果返回之前起作用，且WHERE中不能使用聚合函数。
#### HAVING
HAVING是一个过滤声明，是在查询返回结果集以后对查询结果进行的过滤操作，在HAVING中可以使用聚合函数。
#### GROUP BY
* 用HAVING就一定要和GROUP BY连用，但是用GROUP BY不一定有HAVING。
* 只要条件里面的字段，不是表里已有的字段就需要用HAVING。
* WHERE子句在聚合前先筛选记录，即在GROUP BY子句和HAVING子句前；而HAVING子句在聚合后对组记录进行筛选。
