# Readme
A note about Three-Level Resource ID.

### 三级Resource ID

可以使用形如“DatabaseID-TablePartitionID-RecordID”的三级Resource ID：
- 第1级是Database ID，要求Database ID具有全局唯一性，根据Database ID可以查询到对应的Database Connection Parameters。
- 第2级是Table Partition ID，只要求在对应的Database中具有唯一性，隐含的Resource Type串联Table Partition ID就是表名。
- 第3级是Record ID，只要求在对应的表中具有唯一性。

因为使用“-”符号进行连接和分隔，所以Database ID、Table Partition ID和Record ID可以使用自由的长度。

如果Record ID是多列的形式，可以使用“&”符号连接和分隔多列。

对已经存在的资源进行Read/Update/Delete操作时，只需要根据DatabaseID-PartitionID-RecordID去定位该资源，然后进行处理即可。

对于待创建的资源，要为每一个Resource Type指定一个 Resource Type -> (Database ID, Partition ID) 的映射，以允许新建资源。当当前Record数量快达到上限时或当当前Table Partition数量快达到上限时，应该由一个Capacity Ensurer来创建新的Partition或创建新的Database和Partition并更新这个映射，而应用程序对于这种变更应该是无感知的。

存在一些预定义的常量，例如一个Database中最多允许多少个Table Partition、一个Table Partition中最多允许多少条Record。

### Credits
- Computer Systems: A Programmer's Perspective, Third Edition
- [Page Table, Page Number and Byte Offset - Hcpty](https://github.com/hcpty/page-table-page-number-and-byte-offset)
- [Available, Big and Fast - Hcpty](https://github.com/hcpty/available-big-and-fast)
