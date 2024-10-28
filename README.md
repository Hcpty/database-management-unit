# Readme
A note about Three-Level Resource ID.

### 三级Resource ID

可以使用形如“DatabaseID-PartionID-RecordID”的三级Resource ID：
- 第1级是Database ID，根据Database ID可以查询到对应的表所在的Database的URN。
- 第2级是Partion ID，只要求在对应的Database中具有唯一性，隐含的Resource Type串联Partion ID就是表名。
- 第3级是Record ID，只要求在对应的表中具有唯一性。

这样做会造成处理ID的开销，好处是避免了一个单一的、巨大的表，允许每个表的尺寸都不大，从而获得可以无限增长的容量和稳定的查询速度。

注意如果Record ID是多列的形式，可以使用“&”符号连接多列。

注意由于使用了“-”符号连接，所以Database ID、Partion ID和Record ID不需要根据起始位置和长度进行区分。

注意对于Key-Value Database可以使用“/”连接和分隔表名和Resource ID。

### Credits
- Computer Systems: A Programmer's Perspective, Third Edition
