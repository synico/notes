# Query Parser通用查询参数

Standard, DisMax, eDisMax request query parser都支持的查询参数

#### 1. defType
定义解析请求时使用的查询分析器（Query Parser），默认为DisMax。

#### 2. sort
指定查询结果的排序方式。Solr可以根据文档评分（document scores）排序，也可以对multiValued="false"并且indexed="true"的字段排序。  
1) 排序参数必须包含字段名，用空格分隔排序反向。  
2) 多字段排序用逗号分隔。

#### 3. fq（Filter Query）
定义一个restrict返回文档超集，且不影响score的查询。filter query对于提升复杂查询速度有很大提升。因为每个filter query的结果集都独立的被缓存。  
1) 一个查询可包含多个filter query，这个查询的结果是所有filter query的交集。  
2) 每个查询过滤器的结果集都会独立被缓存，如果使用多个查询过滤器，可考虑合并这些filter query。  
3) 查询过滤器中的特殊字符需要escape和encode为16进制的值。

#### 4. fl（Field List）
控制查询返回结果包含的字段，但仅对已索引（indexed="true"）并存储（stored="true"）的字段有效。定义时，字段以空格或逗号分隔。

#### 5. field name aliases
使用fl=fieldName:displayName的格式改变结果中displayName。

#### 6. cache parameter：默认情况下，Solr会缓存所有queries和filter queries的结果。可以使用cache＝false禁止缓存query结果。

#### 7. debug
1) debug=true：仅返回查询（query）的调试信息  
2) debug=query：仅返回查询（query）的调试信息  
3) debug=timing：返回查询处理各个阶段所耗时间的调试信息  
4) debug=results：返回查询结果（a.k.a explain）相关的调试信息
