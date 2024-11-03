# Readme
A note about DMU (Database Management Unit).

### 数据库管理单元

DMU的特性：
- DMU以表为单位存储记录，其中表具有固定的大小。
- DMU按照表存储的资源的类型对表进行分类，另外，一种资源可能占用很多张表，在这种情况下，如果允许一个数据库存储多种类型的资源，会给Database Administration造成极大的不便，因此，最好让一个数据库只存储一种类型的资源。

地址翻译的过程：
- 应用程序向DMU输入一个地址 (Resource Type, Database Offset, Table Offset, Row Offset)，请求返回对应的数据库连接和表名。
- DMU拥有一张表，其中记录了Database Administrator为每种Resource Type分配的Database，DMU事先建立到这些数据库的连接，然后创建一个connections字典，以Resource Type为键、数组为值，以Database Offset为数组下标、数据库连接为数组元素，connections\[Resource Type\]\[Database Offset\]即为该表对应的数据库连接，字符串"table"串联Table Offset即为该表的表名。

Database Table：
```
Resource Type, Database Offset, Database Connection Arguments
```

地址分配的过程：
- 应用程序请求DMU为一个新资源分配一个地址，要求返回对应的数据库连接和表名。
- DMU拥有一张表，其中记录了Database Administrator对每种Resource Type的分段配置，DMU先读取该配置。DMU还拥有另一张表，其中记录了DMU为每种Resource Type目前已经分配并且在使用的Database和Table，DMU查询对应的Resource Type的最后一个Database中的最后一个Table，然后查看查询的结果：
  - 如果Table Length < Table Size - 1，说明表未满，那么直接返回对应的数据库连接和表名。
  - 否则如果Table Offset < Database Size - 1，说明数据库未满，那么在当前数据库中创建一个相同类型且Table Offset为当前Table Offset + 1的表，并在Allocation Table中添加一条记录，然后返回对应的数据库连接和表名。
  - 否则重新读取一遍Connection Table，查询可能存在的Database Administrator最近为该Resource Type新分配的数据库，如果有的话，就将到新分配的数据库的连接以Database Offset为下标添加到connections\[Resource Type\]数组中，然后选取下标为当前Database Offset + 1的数据库连接，创建一个相同类型且Table Offset为0的表，并在Allocation Table中添加一条记录，然后返回对应的数据库连接和表名。

Segmenting Table：
```
Resource Type, Database Size, Table Size, Table Creation Script
```

Allocation Table：
```
Resource Type, Database Offset, Table Offset
```

其他注意事项：
- DMU允许Database Administrator在DMU运行时在Connection Table中新增记录，以实现不停机扩容。
- 如果数据库不提供设置限制表大小的接口，那么可能会发生Table Length超出DMU配置的限制的现象，DMU允许这种现象发生。
- DMU本身使用JSON文件存储各种配置表。

### Credits
- [DB-Engines Ranking - popularity ranking of database management systems](https://db-engines.com/en/ranking)
- [Page Table, Page Number and Byte Offset - Hcpty](https://github.com/hcpty/page-table-page-number-and-byte-offset)
