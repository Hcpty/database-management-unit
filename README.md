# Readme
A note about DMU (Dataspace Management Unit).

DMU主要负责地址翻译和地址分配。

### 地址翻译

Resource Allocation Table：

```
Logical Address -> Physical Address
```

其中，Logical Address数据结构包含两个字段：
- Resource Type
- Resource Identifier

其中，Physical Address数据结构包含四个字段：
- Node Number
- Database Number
- Table Number
- Record Number

其中，Resource Identifier是含有语义的、面向用户的资源标识符。

其中，所有的Number都从0开始，并在创建时逐1递增。

注意，Resource Allocation Table可以是分段的，在这种情况下需要并行地查找多张Resource Allocation Table。

### 地址分配

### Credits
- [DB-Engines Ranking - popularity ranking of database management systems](https://db-engines.com/en/ranking)
- [Page Table, Page Number and Byte Offset - Hcpty](https://github.com/hcpty/page-table-page-number-and-byte-offset)
