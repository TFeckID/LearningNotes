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





