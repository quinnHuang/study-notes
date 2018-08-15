# 底层原理
* Data files
* Control files
* UNDO files
* Password files
* Online redo log files

## 数据库连接方式
1. C/S
2. B/S

## 内存结构
1. PGA
2. SGA  
share pool
3. Buffer Cache  
存储data files的副本  
LRU  
LRUW 存放脏数据
4. Redo log Buffer
5. Background Processes: maintains and enforce relationship between physical and memory structure  
    1. Database Writers
    2. System Monitor (SMON): 处理数据库崩溃之后的数据清理和回滚
    3. Process Monitor (PMON): 进程中断或失败后的数据清理和回滚
    4. Check Point (CKPT): 在数据库崩溃时，将内存中已经修改的脏数据写入数据文件
    5. Archiver

## Oracle数据库的内存结构
* Read Consistency (读一致性)  
SCN：System Change Number
* Recovery

## Process of Query Statement
1. Parse the Statement：创建指针，进入SQL Area
2. Bind and Para...
3. Execute
4. Fetch: 可以设置返回的行数

## Cost Based Optimizer (优化器)


## Full Table Scan (全表扫描)
1. no suitable index
2. low selectivity filter
3. small table

## Row ID Scan (行ID扫描)
rowid属性  *
rownum返回的行数

## Join的方式
1. Nested loops: 过滤后存在 small table
2. Sort-merge Join
3. Hash join: 两个表都是 big table

---

# index 索引
B-Tree  
升序排列  
查找的数据少于总数的5%时使用索引更快  
索引中不包含null
## index的结构
* root
    * branch
    * branch
        * leaf
        * leaf ( rowId, column key, key column length, index entry header )

## Index Type
1. unique index: 唯一索引
2. composite index: 组合索引
3. Descending index: 降序索引
4. Reverse key index: 减少并发的冲突

## Index Join Scan
过滤的两个条件都添加了索引

## Bitmap Index
并发性差，容易造成死锁  
适合在唯一值少的字段建立  
and 和 or 连接操作的效率高  
