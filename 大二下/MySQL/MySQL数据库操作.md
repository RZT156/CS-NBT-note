MySQL数据表操作：[[MySQL数据内容操作]]
# 1.DDL
## 查询
查看所有数据库
`show databases;
查看当前处于哪个数据库
`select database();
## 创建
`CREATE DATABASE [if not exists] 数据库名 [default charset 字符集];
if not exists: 当库不存在时创建
# 删除
`DROP DATABASE [if exists] 数据库名;
# 选择使用
`use 数据库名;
# 2.DML
# 3.DQL
# 4.DCL