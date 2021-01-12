[https://www.bilibili.com/video/BV1NJ411J79W?p=5]

1.7、 连接数据库
----------------------
命令行连接！
```SQL
mysql -uroot -p123456 --连接数据库

update mysql.user set authentication_string=password('123456') where user='root' and Host = 'localhost';   --修改用户密码

flush privileges;  --刷新权限

------------
--所有语句都使用;结尾

show datases; --查看所有的数据库

mysql>use school --切换数据库 use 数据库名

--
show tables; --查看数据库中所有的表

describe student; --显示数据库中所有的表的信息

create database westos;   --创建一个新数据库

exit;  --退出连接

--单行注释
'#' == '--'
/* 
多行注释
dsadf
dsafdsf
dgfhj
*/ 
```

数据库xxx语言 （CRUD增删改查，cv程序员，API程序员，CRUD程序员） 业务

DDL--数据库定义语言

DML--数据库操作语言

DQL--数据库查询语言
80%

DCL--数据库控制语言

2、操作数据库
----------------------


















