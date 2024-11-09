# Readme
A note about Database Management Unit.

### Database Management Unit

Table Catalog Database：

```
Table, Database Offset, Database Connection Arguments, Weight
```

Bucket Catalog Database:

```
Bucket, Object Storage Offset, Object Storage Authentication Arguments, Weight
```

其他注意事项：
- Database通常不擅长文件存储，Database通常应该附带额外的Object Storage以支援文件存储。

### Credits
- [Page Tables, Page Number and Byte Offset - Hcpty](https://github.com/Hcpty/page-tables-page-number-and-byte-offset)
