# Readme
A note about Database Management Unit.

### Database Management Unit

Table Catalog Database：

```
Table, Database Offset, Database Connection Arguments, Weight
```

Bucket Catalog Database:

```
Bucket, Object Storage Offset, Object Storage Connection Arguments, Weight
```

其他注意事项：
- 一个 (Table, Database Offset) 二元组可以对应多个Partition。
- Database本身不擅长文件存储，Database通常附带额外的Object Storage以支援文件存储。

### Credits
- [Page Tables, Page Number and Byte Offset - Hcpty](https://github.com/Hcpty/page-tables-page-number-and-byte-offset)
