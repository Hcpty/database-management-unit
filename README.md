# Readme
A note about Three-Level Resource ID.

### 三级Resource ID

可以使用形如“DatabaseID-PartionID-ResourceID”的三级Resource ID：
- 第1级是Database ID，根据Database ID可以查询到对应的表所在的Database的URN。
- 第2级是Partion ID，Resource Type串联Partion ID就是表名。
- 第3级是Resource ID，只要求在对应的表中具有唯一性。

这样做会增加查询次数，好处是避免了一个单一的、巨大的表，允许每个表的尺寸都不大，从而获得无限增长的容量和稳定的查询速度。

### Credits
- Computer Systems: A Programmer's Perspective, Third Edition
