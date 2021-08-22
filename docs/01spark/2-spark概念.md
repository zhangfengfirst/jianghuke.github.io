# 窄依赖与宽依赖
## 窄依赖（Narrow Dependency）
- 窄依赖指的是子RDD只依赖于父RDD固定数量的分区。
## 宽依赖（Wide Dependency或Shuffle Dependency）
- 宽依赖只子RDD的每一个分区都依赖于父RDD的所有分区。