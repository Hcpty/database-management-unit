# Readme
A note about Database Management Unit.

### Database Management Unit

Table Catalog Database：

```
Table, Database Offset, Database Connection Arguments, Weight
```

Bucket Catalog Database:

```
Bucket, File Storage Offset, File Storage Connection Arguments, Weight
```

其他注意事项：
- 一个 (Table, Database Offset) 二元组可以对应多个Partition。
- 由于Database本身不擅长存储文件，所以Database通常附带Object Storage以支援文件存储。

### Credits
- [Page Tables, Page Number and Byte Offset - Hcpty](https://github.com/Hcpty/page-tables-page-number-and-byte-offset)
