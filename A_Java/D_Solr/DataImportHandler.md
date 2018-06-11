# Data Import Handler

#### 1. Entity
一个实体被Solr处理生成一组documents。对于RDBMS数据源来说，一个实体对应一个视图或一张表，可通过若干条SQL查询语句得到多行数据（即documents）。

#### 2. Processor
将数据源中提取的数据transform，然后将transform后的数据加入到索引中。

#### 3. Transformer
可用来修改Entity获取的字段信息，或基于Entity获取的字段信息创建新的字段，或基于一条记录生成多条记录（文档）。

#### 4. 配置
DIH配置在solrconfig.xml中。必须包含config参数，因为config定义了DIH的配置文件位置。DIH配置文件中包含数据源信息，获取数据的方法等信息。

#### 5. Entity Processors
提取数据，transform数据，将处理过的数据加入到索引中。对应<entity>标签，<entity>标签有许多子集，如SQL Entity Processor。其中所有<entity>标签的共有属性如下。  
1) datasource：DIH中如配置了多个数据源，则需要明确指定该entity使用的数据源。  
2) name：entity的名称，用来标识Entity的唯一标识。  
3) pk：可选属性，定义entity的主键。仅需要使用data-import时定义。与shema.xml中定义的主键无关，但可用在相同的字段。  
4) processor：默认为SQLEntityProcessor，仅当数据源为非RDBMS时定义其他processor时使用（必须）。  
5) onError：（abort|skip|continue），默认值为abort表示遇到错误中止，skip表示跳过当前document，continue表示忽略错误并继续执行。  
6) preImportDeleteQuery：仅在<document>节点的直接子节点上有效。  
7) postImportDeleteQuery  
8) rootEntity  
9) transformer：可选属性。

#### 6. SQL Entity Processor
1) query：必须，用来查询要处理的记录。  
2) deltaQuery：定义用来执行delta-import的查询，查询需增量更新记录的主键。deltaImportQuery可通过${dataimporter.delta.<column-name>}获取查询出的主键。  
3) parentDeltaQuery：从deltaQuery中获取当前表中更新的行，并把这些行提交给父表。  
4) deletePkQuery  
5) deltaImportQuery  

#### 7. Transformers
transformer在由一个entity返回的document中操作字段。可在<entity>元素的transformer属性中添加需要的transformers，用逗号分隔所需的全部transformers。
