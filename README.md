# Support Apache Hudi by SQL
## 概念
理念最开始来源于 https://issues.apache.org/jira/projects/HUDI/issues/HUDI-481

项目目的主要是能利用SQL的方式或者类SQL的方式去描述和操作Hudi的任务。具体的使用场景可以是：
* 批量更新某个字段的值，并带有部分条件的筛选
* 批量删除含有指定值的行
* truncate一个Hudi表的数据，但是保留其结构信息
* 针对某些pipline的数据处理场景，可以使用SQL模式让数据科学家方便操作已有的数据集
* 等等，待补充

预期的一种表述形式如下：
```scala
# 对象声明
val hudiTable = new HudiTable(path)
hudiTable.update.set("col1 = X").where("col2 = Y")
hudiTable.delete.where("col3 = Z")
hudiTable.commit
```

预期的另一种表述形式如下：
```sql
# SQL模式，可能需要Spark3的支持，还未最后构思好
DELETE FROM tableName WHERE date >= '2020-10-01'
DELETE FROM `/path/` WHERE date >= '2020-10-01'
```