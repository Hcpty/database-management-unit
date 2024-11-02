# Readme
A note about DMU (Dataspace Management Unit).

存储

内存划分为页，数据库划分为表。
Logical Address：(Page Number, Byte Offset)
Logical Address: (Table Number, Row Offset)

为了访问表，还需要数据库连接句柄。
Logical Address: (Database Number, Table Number, Row Offset)
databases = [ ... ]
不使用Table Offset的原因是希望每个Table Number都是全局唯一的。

不同于内存页，表可以是有模式的，特定模式的表只能存储特定模式的记录。
Logical Address: (Resource Type, Database Number, Table Number, Row Offset)
{Resource Type}_databases = [ ... ]

表：
Resource Type, Database Number, Database Connection Arguments

寻址：{Resource Type}_databases[Database Number] . "table"{Table Number} . Row Offset
分配地址：select from ... where Resource Type=? sort by Table Number desc limit 1;
Row Offset使用自增或当前最大+1

删除：逻辑删除
改：先新增后逻辑删

有一个程序负责创建新的Table
Resource Type, Max Tables Per Database, Max Rows Per Table




### Credits
- [DB-Engines Ranking - popularity ranking of database management systems](https://db-engines.com/en/ranking)
- [Page Table, Page Number and Byte Offset - Hcpty](https://github.com/hcpty/page-table-page-number-and-byte-offset)
