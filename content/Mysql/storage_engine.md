---
title: "storage_engine"
date: 2018-12-30 11:31
---


[TOC]



# INNODB

用于处理大量的短期事物，数据存储于表空间table space中

MyISAM 不能保证系统奔溃后可以恢复



## 使用方式

所有InnoDB表的数据和索引放置于同一个表空间中，不方便操作及其备份

或者

每个表单单独使用一个表空间存储表的数据和引擎

```
innodb_file_per_table=ON
```

