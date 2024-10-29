# Readme
A note about Three-Level Resource ID.

### 三级Resource ID

可以使用形如“DatabaseID-TablePartitionID-RecordID”的三级Resource ID：
- 第1级是Database ID，根据Database ID可以查询到对应的Database Connection Parameters。
- 第2级是Table Partition ID，隐含的Resource Type串联Table Partition ID就是表名。
- 第3级是Record ID。

因为使用“-”符号进行连接和分隔，所以Database ID、Table Partition ID和Record ID可以使用自由的长度。如果Record ID是多列的形式，可以使用“&”符号连接和分隔多列。

对已经存在的资源进行Read/Update/Delete操作时，只需要根据DatabaseID-TablePartitionID-RecordID去定位该资源，然后进行处理即可。对于待创建的资源，要为每一个Resource Type指定一个 Resource Type -> (Database ID, Table Partition ID) 的映射，以允许新建资源。当Table Partition或Database的空间不足时，由一个Capacity Ensurer来创建新的Table Partition或Database，然后更新这个映射。

### Credits
- Computer Systems: A Programmer's Perspective, Third Edition
- [Page Table, Page Number and Byte Offset - Hcpty](https://github.com/hcpty/page-table-page-number-and-byte-offset)
- [Available, Big and Fast - Hcpty](https://github.com/hcpty/available-big-and-fast)
