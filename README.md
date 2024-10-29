# Readme
A note about Partitioned-Storage Database.

### 执行分区存储的数据库

逻辑上属于一个Collection的Resource在物理上被分散存储到不同Database Node中的不同Database中的不同的Table中，这种存储方式称为分区存储。

Resource的地址格式是 (Database Node Name, Database Name, Table Name, Record ID)，根据这个地址，可以读写对应的Resource。

### Credits
- Computer Systems: A Programmer's Perspective, Third Edition
- [Page Table, Page Number and Byte Offset - Hcpty](https://github.com/hcpty/page-table-page-number-and-byte-offset)
- [Available, Big and Fast - Hcpty](https://github.com/hcpty/available-big-and-fast)
