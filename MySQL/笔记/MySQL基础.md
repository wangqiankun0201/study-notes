# MySQL基础

## MySQL的结构

现有数据库-->再有表-->再有数据



MySQL可以创建多个数据库，一个库可以创建多张表，一个表有多个列



## 管理数据库

==关键字不区分大小写==

### 查询所有的数据库

show database;

### 创建数据库

create database 数据库名 default character set 字符编码 collate 字符编码校验规则

create database demo default character set utf8 collate utf8_general_ci;

### 修改数据库的字符编码

alter database 数据库名 default character set 字符编码

alter database demo default character set gbk;



### 删除数据库

drop database 数据库名



drop database demo;

### 切换操作的数据库

use 数据库名

use demo;

## 字段的数据类型

### 整型

| MySQL数据类型 | 含义                                   |
| ------------- | -------------------------------------- |
| tinyint       | 1个字节，范围（-128~127）              |
| smallint      | 2个字节，范围（-32768~32767）          |
| mediumint     | 3个字节 范围（-8388608~-8388607）      |
| int           | 4个字节 范围（-2147483648~2147483647） |
| bigint        | 8个字节 范围（+-9.22*10的18次方）      |

### 浮点型

| MySQL数据类型 | 含义                                           |
| ------------- | ---------------------------------------------- |
| float(m,d)    | 单精度浮点型 8位精度(4字节)，m总个数，d小数位  |
| double(m,d)   | 双精度浮点型 16位精度(8字节)，m总个数，d小数位 |

### 定点数

| MySQL数据类型 | 含义                                      |
| ------------- | ----------------------------------------- |
| decimal(m,d)  | 定点数 m<65是总个数，d<30且d小于m，小数位 |

==浮点型在数据库中存放的事近似值，而定点类型在数据库中存放的是精确值==

### 字符串

| MySQL数据类型 | 含义                            |
| ------------- | ------------------------------- |
| char(n)       | 固定长度，最多255个字符         |
| varchar(n)    | 固定长度，最多65525个字符       |
| tinytext      | 可变长度，最多255个字符         |
| text          | 可变长度，最多65535个字符       |
| mediumtext    | 可变长度，最多2的24次方-1个字符 |
| longtext      | 可变长度，最多2的32次方-1个字符 |

### 二进制数据

| MySQL数据类型 | 含义                                    |
| ------------- | --------------------------------------- |
| TINYBLOB      | 可变长度，最多255个字符的二进制数据     |
| BLOB          | 可变长度，最多65535个字符的二进制数据   |
| MEDIUMBLOB    | 可变长度，最多2的24次方-1个二进制数据   |
| LONGBLOB      | 可变长度，最多2的32次方-1个字二进制数据 |

### 日期时间类型

| MySQL数据类型 | 含义                         |
| ------------- | ---------------------------- |
| date          | 日期'2008-12-8'              |
| time          | 时间'12:25:35'               |
| datetime      | 日期时间'2008-12-2 22:06:44' |
| timestamp     | 自动存储记录修改时间         |

## 管理表

### 查看当前操作的数据库有哪些表

show tables;

### 创建表

create table 表名（

字段名 字段类型 [not null] [auto_increment],

字段名 字段类型，

primary key(字段名)

）



create table student(

id int not null,

name varchar(100),

age int(2),

primary key(id)

)

### 修改表

#### 给表添加一个字段

alter table 表名 add column 字段名 字段类型；



alter table student add column sex varchar(2);



#### 给表添加多个字段

alter table 表名 add 字段名 字段类型，add 字段名 字段类型；



alter table student add a int add b int,add c int;

#### 修改字段数据类型

alter table 表名 modify column 字段名 字段类型；



alter table student modify column sex char(4);

#### 修改字段的名称

alter table 表名 change column 原字段名 新字段名 字段的数据类型；



alter table student change column a a1 int;



#### 删除表的一到多个字段

alter table 表名 drop column 字段名；

alter table 表名 drop column 字段名，drop column 字段名；



alter table student drop column a1;

alter table student drop column b,drop column c;



#### 修改表名

alter table 原表名 rename to 新表名;



alter table student rename to stu;



### 删除表

drop table 表名

drop table student;

### 查看表结构

describe 表名;

describe student;



## 管理数据

### 查询表的所有数据

select * from 表名



select * from student;



### 给表插入数据

insert into 表名 values(字段1的值，字段2的值,......)；

insert into student value(1,'张三',15,'男')；



insert into 表名（字段1，字段2，...字段n）values（字段1的值，字段2的值，.....字段n的值）；

insert into 表名（字段1，字段3，字段5）values（字段1的值，字段3的值，字段5的值）；

insert into student(id,name,age) values(2,'李四',15);





insert into 表名 values (字段1的值，字段2的值，....字段n的值),

(字段1的值，字段2的值，....，字段n的值),

.....

(字段1的值，字段2的值，.....,字段n的值);

insert into student values(4,'lucky',15,'女'),(5,'小明',15,'男'),(6,'小红',16,‘女)；

==在插入一个数据时，如果一个字段是自动递增的，可以不用插入这个字段的值，而由数据库自己填充计算。==



### 修改数据

#### 修改一到多个指定字段的所有行的值

update 表名 set 字段名 = 值,字段名 = 值，...,字段名 = 值；

updata student set class = '二班';



#### 按条件修改指定字段的值

updata 表名 set 字段名 = 值 where 字段名 = 值；



update student set sex = '男' where id = 2;

#### 按条件修改一到多个指定字段的所有行的值

==如果不加where 条件，会改变当前所有行的数据==



update 表名 set 字段名 = 值，字段名=值，...，字段名 = 值 where 字段名  = 值；



update student set name = '张三',age = 12,sex = '男',class = '一班' where id = 3;



### 删除表

#### 按条件删除

delete from 表名 where 字段名 = 值；

delete form student where id = 2;



#### 整体删除

删除表当前的所有行数据

delete from 表名；

delete from student;

==如果表中有字段是字段递增类型的，使用delete删除全表后，自动递增的起始点保留。==

==如果想要让自动递增也回归初始状态，需要把表drop掉，然后重新建表。==

==如果表中有字段是字段递增类型的时候，删除中间的某条数据，不会影响递增的叠加==



