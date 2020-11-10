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