# SQL：从入门到夺舍

### 关系模型

---

#### 主键

主键可唯一确定表中的一条记录，主键的设定遵循以下原则

1. 应尽量与业务无关
2. 主键可以设为自增的BIGINT类型，或使用GUID算法得到唯一标识的值
3. 主键不允许有重复值
4. 一个表中可以有多个主键，称为联合主键，联合主键中的某一个或几个可以重复，但联合主键整体不能重复

---

#### 外键

外键可将本表的一个字段与其他表的字段相连接，实现多表查询

- 定义外键的语句

```mysql
ALTER TABLE <table_name>
ADD CONSTRAINT fk_<column_name> 
FOREIGN KEY (<column_name>)
REFERENCES <foreign_table_name> (column_name);
```

- 删除一个外键的语句

```mysql
ALTER TABLE <table_name>
DROP FOREIGN KEY fk_<column_name>;
```

---

#### 索引

对于大量重复率低的数据，可以添加索引来提升查询速度，索引高效的前提是所在字段的数据必须是尽量散列的

- 创建索引的语句

  ```mysql
  ALTER TABLE <table_name>
  ADD INDEX <index_name> (column1,column2, ...);
  ```

- 删除索引的语句

  ```mysql
  ALTER TABLE <table_name>
  DROP INDEX <index_name>;
  ```

> 唯一索引

对于具有业务含义，不宜作为主键，又有唯一性约束要求的字段，可以创建唯一索引，创建有唯一索引的列，不能存储相同的两条记录。

- 创建唯一索引的语句

  ```mysql
  ALTER TABLE <table_name>
  ADD UNIQUE INDEX <index_name> (column1,column2, ...);
  ```

- 删除唯一索引的语句

  ```mysql
  ALTER TABLE <table_name>
  DROP INDEX <index_name>
  ```

若只想对某列添加唯一性约束，但不创建索引

- 添加唯一性约束的语句

  ```mysql
  ALTER TABLE <table_name>
  ADD CONSTRAINT <uni_name> UNIQUE (column1,column2, ...);
  ```

- 删除唯一约束的语句

  ```mysql
  ALTER TABLE students
  DROP INDEX <uni_name>;
  ```

### 查询

---

#### 基本查询

使用SELECT 语句进行基本的查询

```mysql
SELECT * FROM <table_name>  #查询表内所有信息
```

#### 条件查询

- 通过WHERE 关键字来限定查询的条件，其语法为

```mysql
SELECT * FROM <表名> WHERE <条件表达式>
```

- 多个条件表达式可用`AND`, `OR` , `NOT`逻辑算符连接

```mysql
SELECT * FROM <表名> WHERE <条件表达式1> AND <条件表达式2>
SELECT * FROM <表名> WHERE <条件表达式> OR <条件表达式2>
SELECT * FROM <表名> WHERE NOT <条件表达式>
```

条件运算按照`NOT`、`AND`、`OR`的优先级进行，即`NOT`优先级最高，其次是`AND`，最后是`OR`。加上括号可以改变优先级。

- 常用的条件表达式

| 条件                 | 表达式举例1     |   表达式举例2    |                       说明                        |
| :------------------- | :-------------- | :--------------: | :-----------------------------------------------: |
| 使用=判断相等        | score = 80      |   name = 'abc'   |             字符串需要用单引号括起来              |
| 使用>判断大于        | score > 80      |   name > 'abc'   | 字符串比较根据ASCII码，中文字符比较根据数据库设置 |
| 使用>=判断大于或相等 | score >= 80     |  name >= 'abc'   |                                                   |
| 使用<判断小于        | score < 80      |  name <= 'abc'   |                                                   |
| 使用<=判断小于或相等 | score <= 80     |  name <= 'abc'   |                                                   |
| 使用<>判断不相等     | score <> 80     |  name <> 'abc'   |                                                   |
| 使用LIKE判断相似     | name LIKE 'ab%' | name LIKE '%bc%' | %表示任意字符，例如'ab%'将匹配'ab'，'abc'，'abcd' |

#### 投影查询

查询指定的列，返回结果与原表结构不符合的查询称为投影查询

投影查询语句

```mysql
SELECT column1,column2, ... FROM <table_name>;
```

可以对结果集的表头进行重命名

```mysql
SELECT column1 col_name1, column2 col_name2, ... FROM <table_name>;
```

#### 查询结果排序

在查询语句后面加`ORDER by`，并在后面添加想要排序的关键字，如

```mysql
SELECT * FROM student ORDER BY Id;  /*根据Id字段排序*/
```

排序默认按升序排列。如果要按降序排列，在`Order by` 后添加`DESC`关键字，例

```mysql
SELECT * FROM student ORDER BY Id DESC; /*按Id降序排序*/
```

可以按照多个关键字排序

```mysql
SELECT * FROM student ORDER BY Id DESC,score DESC;
```

当存在`where`关键字时，`ORDER BY`关键字要放在最后

```mysql
SELECT * FROM student where score > 90 ORDER BY score DESC;
```

#### 分页查询

使用SELECT查询时，如果结果集数据量很大，比如几万行数据，放在一个页面显示的话数据量太大，不如分页显示，每次显示100条。要实现分页功能，实际上就是从结果集中显示第1~100条记录作为第1页，显示第101~200条记录作为第2页，以此类推。因此，分页实际上就是从结果集中“截取”出第M~N条记录。这个查询可以通过`LIMIT <M> OFFSET <N>`子句实现。例：

```mysql
SELECT * FROM student ORDER BY score LIMIT 3 OFFSET 0
```

其中，`<M>`表示每页多少条记录，`<N>`表示偏移量。上述查询`LIMIT 3 OFFSET 0`表示，对结果集从0号记录开始，最多取3条。注意SQL记录集的索引从0开始。如果要查询第2页，那么我们只需要“跳过”头3条记录，也就是对结果集从3号记录开始查询，把`OFFSET`设定为3。

分页查询的关键在于，首先要确定每页需要显示的结果数量`pageSize`（这里是3），然后根据当前页的索引`pageIndex`（从1开始），确定`LIMIT`和`OFFSET`应该设定的值：

- `LIMIT`总是设定为`pageSize`；
- `OFFSET`计算公式为`pageSize * (pageIndex - 1)`。

这样就能正确查询出第N页的记录集。

`OFFSET`超过了查询的最大数量并不会报错，而是得到一个空的结果集。

注意

`OFFSET`超过了查询的最大数量并不会报错，而是得到一个空的结果集。`OFFSET`是可选的，如果只写`LIMIT 15`，那么相当于`LIMIT 15 OFFSET 0`。

在MySQL中，`LIMIT 15 OFFSET 30`还可以简写成`LIMIT 30, 15`。

使用`LIMIT <M> OFFSET <N>`分页时，随着`N`越来越大，查询效率也会越来越低。

#### 聚合查询

聚合查询可以统计一张表中某些列的数据量，如学生总数，分数的平均值等，要实现这样的效果，SQL提供了内置的聚合函数可供实现。

```mysql
SELECT COUNT(*) FROM students; --计算学生总数，COUNT(*)为聚合函数
```

除了`COUNT()`函数外，SQL还提供了如下聚合函数：

| 函数 | 说明                                   |
| :--- | :------------------------------------- |
| SUM  | 计算某一列的合计值，该列必须为数值类型 |
| AVG  | 计算某一列的平均值，该列必须为数值类型 |
| MAX  | 计算某一列的最大值                     |
| MIN  | 计算某一列的最小值                     |

注意，`MAX()`和`MIN()`函数并不限于数值类型。如果是字符类型，`MAX()`和`MIN()`会返回排序最后和排序最前的字符。如果聚合查询的`WHERE`条件没有匹配到任何行，`COUNT()`会返回0，而`SUM()`、`AVG()`、`MAX()`和`MIN()`会返回`NULL`。

##### 分组聚合

通过`GROUP BY`字句，可以将某些列分别聚合查询，如

```mysql
SELECT COUNT(*) num FROM students GROUP BY class_id; --按照班级分别统计人数
```

注意，聚合查询的列中，只能放入用于分组的列。

#### 多表查询

SELECT查询不但可以从一张表查询数据，还可以从多张表同时查询数据。查询多张表的语法是：`SELECT * FROM <表1> <表2>`。

例如，同时从`students`表和`classes`表的“乘积”，即查询数据，可以这么写：

```mysql
SELECT * FROM student,classes;
```

这种一次查询两个表的数据，查询的结果也是一个二维表，它是`students`表和`classes`表的“乘积”，即`students`表的每一行与`classes`表的每一行都两两拼在一起返回。结果集的列数是`students`表和`classes`表的列数之和，行数是`students`表和`classes`表的行数之积。

这种多表查询又称笛卡尔查询，使用笛卡尔查询时要非常小心，由于结果集是目标表的行数乘积，对两个各自有100行记录的表进行笛卡尔查询将返回1万条记录，对两个各自有1万行记录的表进行笛卡尔查询将返回1亿条记录。

注意，多表查询时，要使用`表名.列名`这样的方式来引用列和设置别名，这样就避免了结果集的列名重复问题。但是，用`表名.列名`这种方式列举两个表的所有列实在是很麻烦，所以SQL还允许给表设置一个别名，让我们在投影查询中引用起来稍微简洁一点：

```mysql
SELECT
    s.id sid,
    s.name,
    s.gender,
    s.score,
    c.id cid,
    c.name cname
FROM students s, classes c;
```

`FROM`子句给表设置别名的语法是`FROM <表名1> <别名1>, <表名2> <别名2>`。这样我们用别名`s`和`c`分别表示`students`表和`classes`表。

#### 连接查询

连接查询是另一种类型的多表查询。连接查询对多个表进行JOIN运算，简单地说，就是先确定一个主表作为结果集，然后，把其他表的行有选择性地“连接”在主表结果集上。

连接查询的关键字为`JOIN`，连接查询包括以下查询

- 内连接查询，关键字为`INNER JOIN`，语法为：

  ```mysql
  SELECT s.id, s.name, s.class_id, c.name class_name, s.gender, s.score
  FROM students s
  INNER JOIN classes c
  ON s.class_id = c.id;
  ```

  内连接的写法为：

  1. 先确定主表，仍然使用`FROM <表1>`的语法；
  2. 再确定需要连接的表，使用`INNER JOIN <表2>`的语法；
  3. 然后确定连接条件，使用`ON <条件...>`，这里的条件是`s.class_id = c.id`，表示`students`表的`class_id`列与`classes`表的`id`列相同的行需要连接；
  4. 可选：加上`WHERE`子句、`ORDER BY`等子句。

- 外连接查询，关键字为`OUTER JOIN`，分为左外连接`LEFT OUTER JOIN`，右外连接`RIGHT OUTER JOIN`，全外连接`FULL OUTER JOIN`。

  - 左外连接：`LEFT OUTER JOIN`返回左表都存在的行，若左边存在的行中有右表不存在的字段，则用NULL填充

  - 右外连接：`RIGHT OUTER JOIN`返回右表都存在的行。如果某一行仅在右表存在，那么结果集就会以`NULL`填充剩下的字段。

  - 全外连接：`NULL OUTER JOIN`会把两张表的所有记录全部选择出来，并且，自动把对方不存在的列填充为`NULL`。

  - 三个外连接查询的区别，假设查询语句如下所示：

    ```mysql
    SELECT ... FROM tableA ??? JOIN tableB ON tableA.column1 = tableB.column2;
    ```

    我们把tableA看作左表，把tableB看成右表，那么INNER JOIN是选出两张表都存在的记录：

    ![inner-join](https://www.liaoxuefeng.com/files/attachments/1246892164662976/l)

    LEFT OUTER JOIN是选出左表存在的记录：

    ![left-outer-join](https://www.liaoxuefeng.com/files/attachments/1246893588481376/l)

    RIGHT OUTER JOIN是选出右表存在的记录：

    ![right-outer-join](https://www.liaoxuefeng.com/files/attachments/1246893609222688/l)

    FULL OUTER JOIN则是选出左右表都存在的记录：

    ![full-outer-join](https://www.liaoxuefeng.com/files/attachments/1246893632359424/l)

### 修改数据

---

#### 增加数据

向数据库总增加数据的操作，关键字为`INSERT`，其语法为

```mysql
INSERT INTO <表名> (字段1, 字段2, ...) VALUES (值1, 值2, ...);
```

可以一次性添加多条记录，只需要在`VALUES`子句中指定多个记录值，每个记录是由`(...)`包含的一组值

```mysql
INSERT INTO <表名> (字段1, 字段2, ...) VALUES (值1, 值2, ...),(值1, 值2, ...), ...;
```

#### 更新数据

要更新数据库中已存在的数据，需要用`UPDATE`关键字。其基本语法为

```mysql
UPDATE <表名> SET 字段1=值1, 字段2=值2, ... WHERE ...;
```

`UPDATE`语句可以没有`WHERE`条件，没有`WHERE`条件的`UPDATE`语句会更新整个表的数据，所以，在执行`UPDATE`语句时，最好先用`SELECT`语句来测试`WHERE`条件是否筛选出了期望的记录集，然后再用`UPDATE`更新。

#### 删除数据

要删除数据库中的数据，需要使用`DELETE`关键字。其基本语法为

```mysql
DELETE FROM <表名> WHERE ...;
```

不带`WHERE`条件的`DELETE`语句会删除整个表的数据，所以，在执行`DELETE`语句时，最好先用`SELECT`语句来测试`WHERE`条件是否筛选出了期望的记录集，然后再用`DELETE`删除。

### MySQL管理命令

---

1. 登录MySQL数据库

   ```mysql
   mysql -h <地址> -u root -p --地址可选，如不指名，则连接本地数据库
   ```

2. 数据库操作

   ```mysql
   SHOW DATABASES; --列出所有的数据库
   CREATE DATABASE <databases_name>; --创建指定名字的数据库
   DROP DATABASE <databases_name>; --删除指定的数据库
   USE <databases_name>; --切换到指定的数据库
   ```

3. 表操作

   ```mysql
   SHOW TABLES; --列出所有的表
   DESC <table_name>; --查看指定的表结构
   SHOW CREATE TABLE <table_name>; --查看创建该表的SQL语句
   DROP TABLE <table_name>; --删除指定的表
   ALTER TABLE students ADD COLUMN birth VARCHAR(10) NOT NULL; --增加一列
   ALTER TABLE students CHANGE COLUMN birth birthday VARCHAR(20) NOT NULL; --修改列名和																			类型
   ALTER TABLE students DROP COLUMN birthday; --删除列
   ```

   