# Readme
A note about Redundant Array of Independent Nodes (RAIN).

### 独立节点冗余阵列

机制：
- Data Striping：把数据进行segmenting，然后把每个segment分别存储到不同的physical node中，通过这种机制，一个大的logical node可以由多个小的physical node虚拟而成，并且可以通过持续地增加physical node来持续地扩展这个logical node的容量，从而实现endless big。
- Node Mirroring：在另一个Node中对目标Node中发生的读写操作进行real time replay，以获得continuous availability。

形式：
- RAIN 0：进行Data Striping。
- RAIN 1：进行Node Mirroring。
- RAIN 01或RAIN 10：同时进行Data Striping和Node Mirroring。

简单易用的是以上三种形式，借助Parity机制还可以实现一些复杂而难用的形式。

一种通用的Data Striping方法：

Resource Allocation Table：
- Resource Type, Resource Identifier -> Logical Address

Logical Address：
- Node Number
- Database Offset
- Table Offset
- Record Offset

Node Table：
- Node Number -> Node Address and Connection Parameters

其中，所有的Number和Offset都从0开始，并在创建时逐1往上递增。

其中，在某些情况下，可以使用特定的Hash Function进行 Resource Type, Resource Identifier -> Logical Address 的映射，以避免使用Datum Allocation Table。

一种通用的Node Mirroring方法：

借助Database Replication实现Node Mirroring。

### Credits
- Computer Systems: A Programmer's Perspective, Third Edition
- [RAID - Wikipedia](https://en.wikipedia.org/wiki/RAID)
- [File Allocation Table - Wikipedia](https://en.wikipedia.org/wiki/File_Allocation_Table)
- [Extent (file systems) - Wikipedia](https://en.wikipedia.org/wiki/Extent_(file_systems))
- [Page Table, Page Number and Byte Offset - Hcpty](https://github.com/hcpty/page-table-page-number-and-byte-offset)
- [DB-Engines Ranking - popularity ranking of database management systems](https://db-engines.com/en/ranking)
- [Available, Big and Fast - Hcpty](https://github.com/hcpty/available-big-and-fast)
