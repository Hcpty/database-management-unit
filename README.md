# Readme
A note about TTMU (Typed Tablespace Management Unit).

### 分类的表空间管理单元

主存以页为单位，而数据库以表为单位。

Table Address包含以下字段：
- Resource Type
- Database Number
- Table Number

Record Address包含以下字段：
- Table Address
- Record Offset

### Credits
- [Page Table, Page Number and Byte Offset - Hcpty](https://github.com/hcpty/page-table-page-number-and-byte-offset)
- [DB-Engines Ranking - popularity ranking of database management systems](https://db-engines.com/en/ranking)
