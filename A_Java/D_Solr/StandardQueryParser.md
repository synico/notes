# Standard Query Parser

优点：standard query parser允许用户定义非常精确的查询。
缺点：相比DisMax query parser而言，standard query parser对于查询语法的正确性有更高的要求（容易因为语法错误而抛出error）。

#### 1. 除query parser支持的通用参数外，支持的参数。
1) q：必要参数，使用标准查询语法定义一个查询。  
2) q.op：指定查询表达式的默认布尔操作符，将覆盖schema.xml中定义的默认值。可选值为"AND"或"OR"（操作符只能为大写）。  
3) df：指定查询的默认字段，将覆盖schema.xml中定义的默认值。

#### 2. Term修饰语
1) wildcard searchers：?和*  
2) fuzzy searchers：~  
3) proximity searchers：~number  
4) range searchers：[ start TO end ]  
5) boosting a term：^  

#### 3. 支持的布尔操作符
1) AND（&&）  
2) NOT（!）  
3) OR（||）  
4) +：符号后的term必须出现在文档中。  
5) -：符号后的term不能出现在文档中。  
6) \：使用blackslash（\）可以转义term中包含的特殊字符。
