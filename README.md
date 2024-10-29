# Readme
A note about Three-Level Resource ID.

### 三级Resource ID

可以使用形如“DatabaseID-PartitionID-RecordID”的三级Resource ID：
- 第1级是Database ID，要求Database ID具有全局唯一性，根据Database ID可以查询到对应的Database Connection Connection。
- 第2级是Partition ID，只要求在对应的Database中具有唯一性，隐含的Resource Type串联Partition ID就是表名。
- 第3级是Record ID，只要求在对应的表中具有唯一性。

这样做会造成处理ID的开销，好处是避免了全局唯一的Record ID，避免了一个单一的、巨大的表，允许每个表的尺寸都不大，从而能够获得可以无限增长的容量和稳定的查询速度。

由于使用“-”符号进行连接和分隔，所以Database ID、Partition ID和Record ID不需要根据起始位置和长度进行定义，可以使用相对自由的长度。

如果Record ID是多列的形式，可以使用“&”符号连接和分隔多列。

如果使用的是Key-Value Database，可以使用“/”连接和分隔表名和Resource ID。

如果使用的是Key-Value Database，可以使用“&”连接和分隔不同的字段。

对已经存在的资源进行Read/Update/Delete操作时，只需要根据DatabaseID-PartitionID-RecordID去定位该资源，然后进行处理即可。

对于待创建的资源，要为每一个Resource Type指定一个 Resource Type -> (Database ID, Partition ID) 的映射，以允许新建资源。当当前Partition快满时或当当前Database快满时，应该由一个Capacity Guarantor来创建新的Partition或创建新的Database和Partition并更新这个映射，而应用程序对于这种变更应该是无感知的。另外，对于进行Data Replication的Database，由于Database的数量会变化，所以相应的复制策略也应作出适当的调整。

### Credits
- Computer Systems: A Programmer's Perspective, Third Edition
- [Page Table, Page Number and Byte Offset - Hcpty](https://github.com/hcpty/page-table-page-number-and-byte-offset)
- [Available, Big and Fast - Hcpty](https://github.com/hcpty/available-big-and-fast)
