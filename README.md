# Readme
A note about DMU (Database Management Unit).

### 数据库管理单元

DMU具有以下特点：
- 以表为单位存储记录，其中表具有固定的大小。
- 按照表存储的资源的类型对表进行分类，另外，一种资源可能占用很多张表，在这种情况下，如果允许一个数据库存储多种类型的资源，会给Database Administration造成极大的不便，因此，最好让一个数据库只存储一种类型的资源。

地址翻译的过程：
- 应用程序向DMU输入一个地址 (Resource Type, Database Number, Table Offset, Record Offset)，请求返回对应的数据库连接和表名。
- DMU拥有一张表，其中记录了Database Administrator事先为每种Resource Type分配的Database，其中包括Database Number和Database Connection Arguments，DMU事先建立到这些数据库的连接，并把这些连接放到一个connections数组中，并以Database Number为数组下标，connections\[Database Number\]即为该表对应的数据库连接，字符串"table"串联Table Offset即为该表的表名。

Connection Table：
```
Resource Type, Database Number, Database Connection Arguments
```

地址分配的过程：
- 应用程序请求DMU为一个新资源分配一个地址，并返回对应的数据库连接和表名。
- DMU拥有一张表，其中记录了关于一个数据库中最多允许存在多少张表以及一个表中最多允许存在多少条记录的配置，DMU事先读取该配置。
- DMU拥有一张表，其中记录了DMU为每种Resource Type已经分配的Database和Table，先查询对应的Resource Type的最后一个Database中的最后一个Table中的最后一个Record，然后查看查询的结果：
  - 如果Record Offset < Table Size - 1，那么直接返回对应的数据库连接和表名。
  - 否则如果Table Offset < Database Size - 1，那么在当前数据库中创建一个相同类型且Table Number为当前Table Number + 1的表，并在Allocation Table中添加一条记录，然后返回对应的数据库连接和表名。
  - 否则重新读取一遍Connection Table，查询Database Administrator是否为该Resource Type新分配了数据库，如果有的话，就将到新分配的数据库的连接以Database Number为下标添加到connections数组中，然后在connections数组中下标为当前Database Number + 1的数据库，创建一个相同类型且Table Number为0的表，并在Allocation Table中添加一条记录，然后返回对应的数据库连接和表名。

Limitation Table：
```
Database Size, Table Size
```

Allocation Table：
```
Resource Type, Database Number, Table Offset
```

Creation Table：
```
Resource Type, Database Creation Script, Table Creation Script
```

其他注意事项：
- 如果使用的数据库不支持对每张表的大小设置限制，那么可能会发生Record Offset超出DMU配置的限制的现象，允许这种现象发生。

### Credits
- [DB-Engines Ranking - popularity ranking of database management systems](https://db-engines.com/en/ranking)
- [Page Table, Page Number and Byte Offset - Hcpty](https://github.com/hcpty/page-table-page-number-and-byte-offset)
