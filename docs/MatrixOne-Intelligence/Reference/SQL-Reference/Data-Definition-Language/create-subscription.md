# **CREATE...FROM...PUBLICATION...**

## **语法说明**

`CREATE...FROM...PUBLICATION...` 是订阅方订阅一个由发布方创建的发布，用来获取发布方的共享数据。

## **语法结构**

```
CREATE DATABASE database_name
FROM account_name
PUBLICATION pubname;
```

## 语法解释

- database_name：订阅方创建的数据库名称。
- pubname：发布方已发布的发布名称。
- account_name：可获取该发布的用户实例名称。

## **示例**

```sql
-- 假设会话 1 为发布方，由发布方先发布一个数据库给另外一个接受方
create database sys_db_1;
use sys_db_1;
create table sys_tbl_1(a int primary key );
insert into sys_tbl_1 values(1),(2),(3);
create view v1 as (select * from sys_tbl_1);
create publication sys_pub_1 database sys_db_1;
mysql> show publications;
+-----------+----------+
| Name      | Database |
+-----------+----------+
| sys_pub_1 | sys_db_1 |
+-----------+----------+
1 row in set (0.01 sec)

-- 再开启一个新的会话，假设会话 2 为订阅方，由订阅方订阅已发布的数据库
mysql -h 127.0.0.1 -P 6001 -u acc1:root -p  --登录该账号
create database sub1 from sys publication pub1;

mysql> create database sub1 from sys publication sys_pub_1;
Query OK, 1 row affected (0.02 sec)

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| system             |
| system_metrics     |
| information_schema |
| mysql              |
| mo_catalog         |
| sub1               |
+--------------------+
6 rows in set (0.00 sec)

mysql> show subscriptions;
+------+--------------+
| Name | From_Account |
+------+--------------+
| sub1 | sys          |
+------+--------------+
1 row in set (0.01 sec)

mysql> use sub1;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> show tables;
+----------------+
| Tables_in_sub1 |
+----------------+
| sys_tbl_1      |
| v1             |
+----------------+
2 rows in set (0.01 sec)

mysql> desc sys_tbl_1;
+-------+---------+------+------+---------+-------+---------+
| Field | Type    | Null | Key  | Default | Extra | Comment |
+-------+---------+------+------+---------+-------+---------+
| a     | INT(32) | NO   | PRI  | NULL    |       |         |
+-------+---------+------+------+---------+-------+---------+
1 row in set (0.01 sec)

mysql> select * from sys_tbl_1 order by a;
+------+
| a    |
+------+
|    1 |
|    2 |
|    3 |
+------+
3 rows in set (0.01 sec)
-- 订阅成功
```

!!! note
    如果需要取消订阅，可以直接删除已订阅的数据库名称，使用 [`DROP DATABASE`](drop-database.md)。