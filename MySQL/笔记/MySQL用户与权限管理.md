# MySQL用户与权限管理

## MySQL的用户管理

### 创建用户

==需要在mysql库的user表操作==

create user '用户名'@'host' identified by '密码'；



**host:**

localhost:本机访问

ip地址：指定的ip地址访问，可以多个ip，用(,)分割

%：任意ip都可以访问





### 查看用户和权限的相关信息

select * from mysql.user;



### 修改用户密码

alter user '用户名'@'主机名'identified by '新密码';



### 修改用户名

update mysql.user set user = '新用户名' where user = '就用户名';



### 删除用户

drop user 用户名；



## MySQL权限管理

### 授予权限



grant 权限 on 数据库.表名 to '用户名'@'host'[with grant option];





**权限：**

所有权限，all privileges.



**数据库和表都可用`*`**填充，表示所有数据库或者所有表





**with grant option:**

加上这段，表示该用户可以给其他用户赋予授权，但是不可以超过该用户已有的权利。





==flush privileges== 刷新权限



### 查看权限

show grants for '用户名'@'host';



### 撤消权限



revoke 权限 on 数据库名.表名 from '用户名'@'host';



