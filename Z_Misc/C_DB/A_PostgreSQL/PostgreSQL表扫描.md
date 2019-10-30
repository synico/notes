## PostgreSQL数据表扫描类型
PostgreSQL中数据表的三种扫描类型，分别是顺序扫描SeqScan，索引扫描IndexScan和位图堆扫描BitmapHeapScan。

### 顺序扫描SeqScan
直接对数据表堆数据 (Heap Data) 进行顺序扫描，适用于选择率较高的场景。postgreSQL根据cost计算来确定使用哪种扫描方式，通常情况下，索引扫描主要执行的操作是随机访问存储设备，在postgreSQL的初始化参数配置中，随机访问的cost是4，而顺序访问的cost是1。粗略的估计，如果通过索引访问的Index Blocks加上Heap Blocks的数量超过顺序访问的Heap Blocks的1//4，那么postgreSQL会选择顺序扫描，而不是索引扫描。
```
ge_apm=# explain analyze select * from asset_info where tenant_uid='1bff2522b1824131938ab4f9b5b0c278';
                                                     QUERY PLAN                                                      
---------------------------------------------------------------------------------------------------------------------
 Seq Scan on asset_info  (cost=0.00..19936.64 rows=95456 width=3044) (actual time=0.187..124.532 rows=94945 loops=1)
   Filter: (tenant_uid = '1bff2522b1824131938ab4f9b5b0c278'::bpchar)
   Rows Removed by Filter: 162626
 Planning time: 2.996 ms
 Execution time: 127.742 ms
(5 rows)
total cost: 19936.64

```
***

### 索引扫描IndexScan
通过访问索引获得元组位置指针后直接访问堆数据，适用于选择率较低的场景。
```
ge_apm=# explain analyze select * from asset_info where id=199607;
                                                          QUERY PLAN                                                           
-------------------------------------------------------------------------------------------------------------------------------
 Index Scan using asset_info_pkey on asset_info  (cost=0.42..8.44 rows=1 width=3044) (actual time=0.013..0.014 rows=1 loops=1)
   Index Cond: (id = 199607)
 Planning time: 0.502 ms
 Execution time: 0.125 ms
(4 rows)
total cost: 8.44

```
***

### 位图堆扫描BitmapHeapScan
需要先通过BitmapIndexScan把符合条件的元组所在的Page (Block) ID存储在Bitmap中，然后再通过Bitmap访问堆数据，适用于选择率不高不低的场景，介于上面两种扫描方式之间。
```
ge_apm=# explain analyze select * from asset_info where site_uid='dae19b2ae6aa451f89073433f2fa32e1';
                                                               QUERY PLAN                                                                
-----------------------------------------------------------------------------------------------------------------------------------------
 Bitmap Heap Scan on asset_info  (cost=715.20..18506.35 rows=19455 width=3044) (actual time=7.664..19.341 rows=19960 loops=1)
   Recheck Cond: (site_uid = 'dae19b2ae6aa451f89073433f2fa32e1'::bpchar)
   Heap Blocks: exact=2789
   ->  Bitmap Index Scan on ix_asset_info_site_uid  (cost=0.00..710.33 rows=19455 width=0) (actual time=6.371..6.371 rows=19960 loops=1)
         Index Cond: (site_uid = 'dae19b2ae6aa451f89073433f2fa32e1'::bpchar)
 Planning time: 0.540 ms
 Execution time: 21.802 ms
(7 rows)
total cost: 18506.35
```
***
