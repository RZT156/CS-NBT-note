MySQL数据库操作：[[MySQL数据库操作]]
# 一、DDL
创建数据表之前，需要先选择数据库`use 数据库名;

## 1.创建表
```
CREATE TABLE 表名称(
字段1 类型 [COMMENT 注释] 约束条件，
字段2 类型 [COMMENT 注释] 约束条件，
......(最后一句不要',')
)[COMMENT 注释];
```

**约束条件**：可以是主键(PRIMARY KEY)、非空(NOT NULL)等；
**注释**：COMMENT '注释内容'；
### 数据类型：
#### 1.数值类型
![[int_float.png]]
#### 2.字符串类型
<table>
<tr>
	<th>数据类型</th>
	<th>描述</th>
	<th>示例</th>
</tr>
<tr>
	<td>char</td>
	<td>固定长度的字符串，长度在创建时指定，不足指定长度时会用空格填充。</td>
	<td>code CHAR(5);</td>
</tr>
<tr>
	<td>varchar</td> 
	<td>用于存储较长的文本数据，有`TINYTEXT`、`TEXT`、`MEDIUMTEXT`和`LONGTEXT`等不同的长度限制。</td>
	<td>name VARCHAR(255);</td>
</tr>
<tr>
	<td>varchar</td> 
	<td>可变长度的字符串，长度在创建时指定，存储时只占用实际字符串长度的空间。</td>
	<td>desc TEXT;</td>
</tr>
<tr>
	<td>blob</td> 
	<td>存储大量的二进制数据，有`TINYBLOB`、`BLOB`、`MEDIUMBLOB`和`LONGBLOB`等不同的长度限制。</td>
	<td>CREATE TABLE test (image_data BLOB);</td>
</tr>
</table>
char(参数); 参数表示长度 
#### 3.日期
![[date.png]]
TIMESRAMP也能记录，但是时间戳到2038年之后就不准了
## 2.查询
**SHOW**
查询当前数据库所有表
`show tables;
查指定表建表语句
`show create table 表名;
**DESC**
查看表结构`describe`,可以缩写成`desc`
`describe 表名;
## 3.修改
### 表字段操作
1) 添加 `ADD
2) 修改 `MODIFY
3) 删除 `DROP
4) 改名 `CHANGE
```
ALTER TABLE 表名 ADD 字段名 类型(长度) [COMMENT 注释] [约束];
ALTER TABLE 表名 MODIFY 字段名 类型(长度);
ALTER TABLE 表名 DROP 字段名;
ALTER TABLE 表名 CHANGE 旧字段名 新字段名 类型(长度) [COMMENT 注释] [约束];
```
### 表操作
改名 `RENAME
`ALTER TABLE 旧数据表名 RENAME( TO) 新数据表名;
## 4.删除
**DROP**
删表
`DROP TABLE [if exists] 表名;

**TRUNCATE**
清空表内容
`TRUNCATE TABLE 表名;
# 二、DML
## 1.插入
**INSERT**
1) 指定字段1，2...添加数据
`INSERT INTO 表名 (字段名1, 字段名2, ...)VALUES (值1, 值2, ...);`
2) 批量添加，前面不变，`VALUES(值1, 值2, ...),(值1, 值2, ...),...;
3) 也可以不带字段名，后面的VALUES(值1, 值2, ...)要与表各属性一一对应
## 2.更新 
**UPDATE**
`UPDATE 表名 SET 字段1=值1, ...[ WHERE 条件];`
## 3.删除 
**DELETE**
`DELETE FROM 表名[ WHERE 条件];
**三类删除对比：[[删除对比]]**
# 三、DQL
```
SELECT   字段/* 
FROM     表
WHERE    条件
GROUP BY 分组字段
HAVING   分组后条件
ORDER BY 排序字段(ASC/DESC)
SELECT 字段名1 AS(可省) 别名1, ...
```
## 条件查询
### 运算符
ANY 任意，ALL  所有
\> ANY 大于最小的，> ALL 大于最大的
\< ANY 小于最大的，< ALL 小于最小的

| 比较运算符 |             | 逻辑运算符           |
| ----- | ----------- | --------------- |
| > 大于  | >= 大于等于     | AND 或 && ==并==  |
| < 小于  | <= 小于等于     | OR 或 \|\| ==或== |
| = 等于  | <> 或 != 不等于 | NOT 或 ! ==非==   |
### WHERE 条件
- **like** 模糊查询（%表示通配符）
- **IN**(...) 锁定多个值
- **BEWTEEN** number1 **AND** number2 (1 < 2) 在区间\[number1, number2]之间
- **DISTINCT** 去除重复值
- **limit** 限制前几 `select 字段 from 表 limit 数量；
#### 聚合函数
`SELECT 聚合函数(字段名) FROM 表名;`
null值不统计
1. AVG
2. COUNT 分组统计
3. MAX
4. MIN
5. SUM
6. UPPER/UCASE 大写
7. LOWER/LCASE 小写
8. LEN/LENGTH 长度
9. ROUND 数值取舍
10. NOW/SYSDATE 当前时间
## 分组查询
**GROUP BY**
`select 字段 from 表 [where 条件]group by 分组字段名 having 分组后条件；`
**WHERE** & **HAVING** 区别
- where分组前过滤，having分组后
- where中不能用聚合函数，having可以
## 排序查询
**ORDER BY** 排序
**ASC**   升序排列
**DESC** 降序排列
`select 字段名 from 表名 order by 字段1 desc, 字段2 desc;`
先满足前面，再满足后面
## 嵌套查询
**IN**
书上有，`select ... from ... where 字段名 in (select ... from ... where ...);`
1. 相关子查询
2. 不相关子查询
  
当`IN`后面括号里**只有一个值**时，`IN`可以写成`=`。
```sql
WHERE id IN (5)
WHERE id = 5
```
**其他情况不能用 `=` 代替 `IN`**：
```sql
-- IN 有多个值，不能改写成 =
WHERE id IN (5, 10, 15)   -- 正确
WHERE id = 5 OR id = 10 OR id = 15   -- 这是等价改写
-- 子查询返回多行，不能直接用 =
WHERE id IN (SELECT user_id FROM orders)   -- 正确
WHERE id = (SELECT user_id FROM orders)    -- 错误：子查询返回多行会报错
```

## 分页查询
不同数据库有不同的实现，MySQL中是**LIMIT**
`limit 起始索引(0-based), 查询数量;`
索引在第一页时可省略。
## 执行顺序
**时序问题！**
having中时序不影响（豆包说的）
```
SELECT   5 
FROM     1
WHERE    2
GROUP BY 3
HAVING   4
ORDER BY 6
LIMIT    7
```

# 四、DCL

# SQL高级语言
## 5.JOIN
多表关联
## 6.UNION
合并结果集
## 8.VIEW
视图

