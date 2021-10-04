# MySQL用户与权限管理

## MySQL的用户管理

### 创建用户

==需要在mysql库的user表操作==

create user '用户名'@'host' identified by '密码'；



**host:**

localhost:本机访问

ip地址：指定的ip地址访问，可以多个ip，用(,)分割

%：任意ip都可以访问

