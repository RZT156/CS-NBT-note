MySQL数据库操作：[[MySQL数据库操作]]
# SQL基础语言
## 数据类型
### 1.数值类型
![[int_float.png]]
### 2.字符串类型
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
### 3.日期
![[date.png]]
TIMESRAMP也能记录，但是时间戳到2038年之后就不准了
# 1.DDL
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
### DROP
删表
`DROP TABLE [if exists] 表名;
### TRUNCATE
清空表内容
`TRUNCATE TABLE 表名;

**三类删除对比：[[删除对比]]**
## 4.INSERT
插入数据

## 5.SELECT
查询数据

## 6.DISTINCT
去除重复值

## 7.WHERE
条件过滤

## 8. AND & OR
运算符

## 9.ORDER BY
排序

## 10.UPDATE
更新

## 11.DELETE
删数据

# SQL高级语言
## 1.LIKE
查找类似值

## 2.IN
锁定多个值

## 3.BEWTEEN
选取区间数据

## 4.AS
别名

## 5.JOIN
多表关联

## 6.UNION
合并结果集

## 7.NOT NULL
非空

## 8.VIEW
视图

# SQL常用函数
1. AVG

2. COUNT

3. MAX

4. MIN

5. SUM

6. GROUP BY

 7. HAVING
句尾连接

8. UPPER/UCASE

9. LOWER/LCASE

10. LEN/LENGTH

11. ROUND
数值取舍

12. NOW/SYSDATE
当前时间