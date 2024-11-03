# Readme
A note about DMU (Database Management Unit).

### 数据库管理单元

DMU有几个特点：
- 以表为单位批量存储记录，其中表具有固定的大小。
- 按照表存储的资源的类型对表进行分类，即让表拥有类型，另外，一个应用程序可能拥有非常多的表，在这种情况下，如果允许一个数据库存储多种类型的资源，这会给Database Administration造成极大的不便，因此，最好让每一个数据库都只存储单一类型的资源，即让数据库也拥有类型。
- 当一个表的空间用尽时，需要新增一个相同类型的表，当对应的数据库的空间也用尽时，需要先申请一个相同类型的数据库，再新增一个相同类型的表。

表地址翻译的过程：
- 应用程序向DMU输入一个表地址 (Resource Type, Database Number, Table Offset)，请求返回对应的数据库连接和表名。
- DMU拥有一张表，其中记录了Database Administrator为每种Resource Type分配的Database，其中包括Database Number和Database Connection Arguments，DMU事先建立了到这些数据库的连接，并把这些连接放到一个connections数组中，并以Database Number为数组下标，connections\[Database Number\]即为该表对应的数据库连接，字符串"table"串联Table Offset即为该表的表名。

Connection Table：
```
Resource Type, Database Number, Database Connection Arguments
```

表地址分配的过程：
- 应用程序请求DMU为一个新资源分配一个表地址，并返回对应的数据库连接和表名。
- DMU拥有一张表，其中记录了DMU为每种Resource Type已经分配的Database和Table，对应的Resource Type的最后一个Database中的最后一个Table即为新资源的表地址，分配表地址的过程中可能伴随着新增表的操作。

Allocation Table：
```
Resource Type, Database Number, Table Offset
```

新增表的操作：
- DMU拥有一张表，其中记录了关于一个数据库中最多允许存在多少张表以及一个表中最多允许存在多少条记录的配置，当新插入的记录的Offset超过了某个数值时，则新增一个相同类型的表，当新创建的表的Offset超过了某个数值时，则先申请一个相同类型的数据库，再新增一个相同类型的表。
- 在Allocation Table中插入一条新的记录。

Limitation Table：
```
Database Size, Table Size
```

### Credits
- [Page Table, Page Number and Byte Offset - Hcpty](https://github.com/hcpty/page-table-page-number-and-byte-offset)
- [DB-Engines Ranking - popularity ranking of database management systems](https://db-engines.com/en/ranking)
