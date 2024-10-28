# Readme
A note about Three-Level Resource ID.

### 三级Resource ID

可以使用形如“DatabaseID-PartionID-RecordID”的三级Resource ID：
- 第1级是Database ID，根据Database ID可以查询到对应的Database Connection Parameters和Database Connection。
- 第2级是Partion ID，只要求在对应的Database中具有唯一性，隐含的Resource Type串联Partion ID就是表名。
- 第3级是Record ID，只要求在对应的表中具有唯一性。

这样做会造成处理ID的开销，好处是避免了全局唯一的Record ID，避免了一个单一的、巨大的表，允许每个表的尺寸都不大，从而能够获得可以无限增长的容量和稳定的查询速度。

由于使用“-”符号进行连接和分隔，所以Database ID、Partion ID和Record ID不需要根据起始位置和长度进行定义，可以使用相对自由的长度。

如果Record ID是多列的形式，可以使用“&”符号连接和分隔多列。

如果使用的是Key-Value Database，可以使用“/”连接和分隔表名和Resource ID。

如果使用的是Key-Value Database，可以使用“&”连接和分隔不同的字段。

### Credits
- Computer Systems: A Programmer's Perspective, Third Edition
- [Page Table, Page Number and Byte Offset - Hcpty](https://github.com/hcpty/page-table-page-number-and-byte-offset)
