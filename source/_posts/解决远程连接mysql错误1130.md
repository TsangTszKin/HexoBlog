---
title: 解决远程连接mysql错误1130
date: 2018-03-19 11:01:55
description: '远程连接Mysql服务器的数据库，错误代码是1130，ERROR 1130: Host xxx.xxx.xxx.xxx  is not allowed to connect to this MySQL server  '
tags: 'mysql'
categories: 数据库

---

远程连接Mysql服务器的数据库，错误代码是1130，ERROR 1130: Host xxx.xxx.xxx.xxx  is not allowed to connect to this MySQL server  
猜想是无法给远程连接的用户权限问题。
这样子操作mysql库，即可解决。 
 
在本机登入mysql后，更改 “mysql” 数据库里的 “user” 表里的 “host” 项，从”localhost”改称'%'即可 

	mysql -u root -p  
	mysql;use mysql;  
	mysql;select 'host' from user where user='root';  
	mysql;update user set host = '%' where user ='root';  
	mysql;flush privileges;  
	mysql;select 'host'   from user where user='root'; 
 
 
第一句：以权限用户root登录  
第二句：选择mysql库  
第三句：查看mysql库中的user表的host值（即可进行连接访问的主机/IP名称）  
第四句：修改host值（以通配符%的内容增加主机/IP地址），当然也可以直接增加IP地址  
如果这步出错"ERROR 1062 (23000): Duplicate entry '%-root' for key 'PRIMARY'" 由说明该记录有了，跳过这步
第五句：刷新MySQL的系统权限相关表  
第六句：再重新查看user表时，有修改。。  
重起mysql服务即可完成。 
