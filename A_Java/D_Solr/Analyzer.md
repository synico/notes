# Analyzer

#### 一般情况下，Analyzer仅处理字段类型为solr.TextField的字段。
1. Analyzer读取包含文本的字段，并生成分词流（token stream）。  
2. Analyzer可能由一个类组成，也可能由一系列tokenizers和filters组成。

#### Analyzer分析（analysis）发生在两种情况下
1. 建立索引时（At index time）：当字段创建时，分析器Analyzer生成的分词流被加入到索引字段中。同时定义该字段一系列术语（terms），包括位置（positions），大小（size）等信息。  
2. 查询时（At query time）：所要查询的值会被分析，同时满足查询条件的结果（存储在字段索引中）也会被分析。
