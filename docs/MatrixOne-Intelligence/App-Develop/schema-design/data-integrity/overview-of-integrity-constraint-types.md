# 约束概述

在 MatrixOne Intelligence 数据库中，为了确保数据的正确性、完整性、有效性，在建表语句中，会对某些列加入限制条件，确保数据库内存储的信息遵从一定的业务规则，这些限制条件被称为约束。例如，如果 DML 语句的执行结果违反了完整性约束（Integrity Constraint），将回滚语句并返回错误消息。

## 完整性约束类型

MatrixOne Intelligence 存在多种约束，不同的约束对于数据库行为有着不同的限制。目前支持的约束都是表级别的约束：

- [NOT NULL 完整性约束](not-null-constraints.md)：

   非空约束是指，某一列的数据不能出现空值（NULL），违反了该限制条件的数据不能被插入或更新在对应列中。在 MatrixOne Intelligence 中，一张表允许有零个、一个或多个非空约束。

- [UNIQUE KEY 完整性约束](unique-key-constraints.md)

   唯一键约束是指，在一张表中存的某一列或多列组合中，被插入或更新的数据行在此列（或列集）的值是唯一的。在 MatrixOne Intelligence 中，一张表中允许存在零个、一个或多个唯一键约束，但与其他关系型数据库不同的是，MatrixOne Intelligence 的唯一键约束也必须非空。

- [PRIMARY KEY 完整性约束](primary-key-constraints.md)

   主键约束是指，在一张表中存的某一列或多列组合中，每一数据行都可以由某一个键值唯一地确定且非空的，并且主键约束在一张表中最多只能有 1 个。

- [FOREIGN KEY 完整性约束](foreign-key-constraints.md)

   外键约束是指，在一张表中存的某一列或多列组合中，被另一张表中的某一列或多列所引用，被引用表通常称为父表，引用表称为子表。子表引用父表的对应列的数据，只能是父表的数据或空值，这种约束被称为外键约束。

- [AUTO INCREMENT 自增约束](auto-increment-integrity.md)

   自增约束是一种用于在表中自动为一个列生成唯一标识值的特性。它允许你在插入新行时，自动为指定的自增列生成一个递增的唯一值。
