# Readme
A note about DMU (Dataspace Management Unit).

DMU用于管理Dataspace，主要负责把Logical Address翻译成Physical Address，以及为新的 (Resource Type, Resource Identifier) 二元组分配新的Physical Address。

### Logical Address

Logical Address数据结构包含两个字段：
- Resource Type
- Resource Identifier

其中，Resoruce Identifier是富含语义的、公开的、面向用户的资源标识符。

### Resource Allocation Table

Resource Allocation Table：

Logical Address -> Physical Address

其中，Physical Address数据结构包含四个字段：
- Node Number
- Database Offset
- Table Offset
- Record Offset

其中，所有的Number和Offset都从0开始，并在创建时逐1往上递增。

Resource Allocation Table是DMU私有的。

### Node Database Table

Node Database Table：

Node Number, Database Offset -> Node Address, Database Connection Arguments

Node Database Table是DMU和应用程序共享的。

### Credits
- [Page Table, Page Number and Byte Offset - Hcpty](https://github.com/hcpty/page-table-page-number-and-byte-offset)
- [RAID - Wikipedia](https://en.wikipedia.org/wiki/RAID)
- [File Allocation Table - Wikipedia](https://en.wikipedia.org/wiki/File_Allocation_Table)
- [Extent (file systems) - Wikipedia](https://en.wikipedia.org/wiki/Extent_(file_systems))
- [DB-Engines Ranking - popularity ranking of database management systems](https://db-engines.com/en/ranking)
- [Available, Big and Fast - Hcpty](https://github.com/hcpty/available-big-and-fast)
