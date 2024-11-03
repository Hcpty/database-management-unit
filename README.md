# Readme
A note about TTMU (Typed Tablespace Management Unit).

### 分类的表空间管理单元

分类的表空间管理含有两层意思：
- 数据库以表为单位批量存储记录。
- 按照表存储的资源的类型对表进行分类，即让表拥有类型。

一个应用程序可能拥有非常多的表，在这种情况下，如果允许一个数据库存储多种类型的资源，会让Database Administration极为不便，所以令每一个数据库都只存储单一类型的资源，即让数据库也拥有类型。

### Credits
- [Page Table, Page Number and Byte Offset - Hcpty](https://github.com/hcpty/page-table-page-number-and-byte-offset)
- [DB-Engines Ranking - popularity ranking of database management systems](https://db-engines.com/en/ranking)
