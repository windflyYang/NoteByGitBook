**SQL**
SQL 可以分为两个部分：数据操作语言 (DML) 和 数据定义语言 (DDL)。

查询和更新指令构成了 SQL 的 DML 部分：
- SELECT - 从数据库表中获取数据
- UPDATE - 更新数据库表中的数据
- DELETE - 从数据库表中删除数据
- INSERT INTO - 向数据库表中插入数据

SQL 的数据定义语言 (DDL) 部分使我们有能力创建或删除表格。我们也可以定义索引（键），规定表之间的链接，以及施加表间的约束。
SQL 中最重要的 DDL 语句:

- CREATE DATABASE - 创建新数据库
- ALTER DATABASE - 修改数据库
- CREATE TABLE - 创建新表
- ALTER TABLE - 变更（改变）数据库表
- DROP TABLE - 删除表
- CREATE INDEX - 创建索引（搜索键）
- DROP INDEX - 删除索引

**SELECT**
SELECT 列名称 FROM 表名称
选取多列也可以逗号隔开
SELECT 列名1，列明2 FROM 表名称
SELECT * FROM 表名称 //选取所有的列

SQL SELECT DISTINCT 语句  关键词 DISTINCT 用于返回唯一不同的值
SELECT DISTINCT 列名称 FROM 表名称

WHERE 子句用于规定选择的标准。
操作符|描述
--|:--:|--:
=|等于
<>|不等于
>|打于
<|小于
>=|大于等于
<=|小于等于
BETWEEN|某个范围内
LIKE|搜索某种模式

**INSERT INTO 语句**
INSERT INTO 表名称 VALUES (值1, 值2,....)//插入新的行
INSERT INTO table_name (列1, 列2,...) VALUES (值1, 值2,....)//指定所要插入的列

**UPDARTE**
UPDATE 表名称 SET 列名称 = 新值 WHERE 列名称 = 某值
**DELETE 语句**
DELETE FROM 表名称 WHERE 列名称 = 值
不删除表结构的情况下删除表中的所有数据
DELETE FROM table_name 
DELETE * FROM table_name

**SQL 高级**
TOP 子句用于规定要返回的记录的数目。
SELECT TOP number|percent column_name(s)
FROM table_name
***MySQL 和 Oracle 中的 SQL SELECT TOP 是等价的***
MySQL
SELECT column_name(s)
FROM table_name
LIMIT number
ORACLE
SELECT column_name(s)
FROM table_name
WHERE ROWNUM <= number
**LIKE**
- 'N%' 以N开头
- '%g' 以g结尾
- '%lon%' 包含lon
-  NOT LIKE '%lon%'  不包含

**SQL 通配符**
通配符|描述
--|:--:|--:
%|替代一个或多个字符
_|仅替代一个字符
[charlist]|字符列中的任何单一字符
[^charlist]或者[!charlist]|不在字符列中的任何单一字符

IN 操作符允许我们在 WHERE 子句中规定多个值。
SELECT * FROM Persons
WHERE LastName IN ('Adams','Carter')

***重要事项：不同的数据库对 BETWEEN...AND 操作符的处理方式是有差异的。某些数据库会列出介于 "Adams" 和 "Carter" 之间的人，但不包括 "Adams" 和 "Carter" ；某些数据库会列出介于 "Adams" 和 "Carter" 之间并包括 "Adams" 和 "Carter" 的人；而另一些数据库会列出介于 "Adams" 和 "Carter" 之间的人，包括 "Adams" ，但不包括 "Carter" 。所以，请检查你的数据库是如何处理 BETWEEN....AND 操作符的！***
SQL join 用于根据两个或多个表中的列之间的关系，从这些表中查询数据。

UNION 操作符用于合并两个或多个 SELECT 语句的结果集。
请注意，UNION 内部的 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每条 SELECT 语句中的列的顺序必须相同。

SQL SELECT INTO 语句可用于创建表的备份复件。