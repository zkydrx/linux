    如何在Linux下卸载MySQL数据库呢？ 下面总结、整理了一下Linux平台下卸载MySQL的方法。 MySQL的安装主要有三种方式：二进制包安装（Using Generic Binaries）、RPM包安装、源码安装。对应不同的安装方式，卸载的步骤有些不同。文章中如有不足或不对的地方，敬请指出或补充！



RPM包安装方式的MySQL卸载

 

1： 检查是否安装了MySQL组件。

[root@DB-Server init.d]# rpm -qa | grep -i mysql

MySQL-devel-5.6.23-1.linux_glibc2.5

MySQL-client-5.6.23-1.linux_glibc2.5

MySQL-server-5.6.23-1.linux_glibc2.5

![](https://github.com/zkydrx/images/blob/master/sql/1.png?raw=true)

如上所示，说明安装了MySQL 5.6.23这个版本的client、server、devel三个组件。

 

2： 卸载前关闭MySQL服务

 

- 方法1

[root@DB-Server init.d]# service mysql status
 MySQL running (25673)[  OK  ]
[root@DB-Server init.d]# service mysql stop
 Shutting down MySQL..[  OK  ]
[root@DB-Server init.d]# service mysql status
 MySQL is not running[FAILED]


![](https://github.com/zkydrx/images/blob/master/sql/2.png?raw=true)

- 方法2

[root@DB-Server init.d]# ./mysql status
 MySQL running (26215)[  OK  ]
[root@DB-Server init.d]# ./mysql stop
 Shutting down MySQL..[  OK  ]
[root@DB-Server init.d]# ./mysql status
 MySQL is not running[FAILED]
[root@DB-Server init.d]# 
![](https://github.com/zkydrx/images/blob/master/sql/3.png?raw=true)

[root@DB-Server init.d]# chkconfig --list | grep -i mysql

mysql 0:off 1:off 2:on 3:on 4:on 5:on 6:off

[root@DB-Server init.d]# 

 

3. 收集MySQL对应的文件夹信息

[root@DB-Server init.d]# whereis mysql

mysql: /usr/bin/mysql /usr/include/mysql /usr/share/mysql /usr/share/man/man1/mysql.1.gz

最好实用find命令查看MySQL数据库相关的文件，方便后面彻底删除MySQL。

[root@DB-Server init.d]# find / -name mysql
/etc/rc.d/init.d/mysql
/etc/logrotate.d/mysql
/var/lock/subsys/mysql
/var/lib/mysql
/var/lib/mysql/mysql
/usr/include/mysql
/usr/include/mysql/mysql
/usr/bin/mysql
/usr/share/mysql
/usr/lib64/mysql
![](https://github.com/zkydrx/images/blob/master/sql/4.png?raw=true)

 

4： 卸载删除MySQL各类组件

[root@DB-Server init.d]# 
[root@DB-Server init.d]# rpm -ev MySQL-devel-5.6.23-1.linux_glibc2.5
[root@DB-Server init.d]# rpm -ev MySQL-server-5.6.23-1.linux_glibc2.5
You have new mail in /var/spool/mail/root
[root@DB-Server init.d]# rpm -ev MySQL-client-5.6.23-1.linux_glibc2.5
[root@DB-Server init.d]#
![](https://github.com/zkydrx/images/blob/master/sql/5.png?raw=true)

 

5：删除MySQL对应的文件夹

 

检查各个MySQL文件夹是否清理删除干净。

[root@DB-Server init.d]# whereis mysql
mysql:
[root@DB-Server init.d]# find / -name mysql
/var/lib/mysql
/var/lib/mysql/mysql
/usr/lib64/mysql
[root@DB-Server init.d]# rm -rf /var/lib/mysql
[root@DB-Server init.d]# rm -rf /var/lib/mysql/mysql
[root@DB-Server init.d]# rm -rf /usr/lib64/mysql
[root@DB-Server init.d]# 
6：删除mysql用户及用户组

如果有必要，删除mysql用户以及mysql用户组。

[root@DB-Server ~]# more /etc/passwd | grep mysql
mysql:x:101:501::/home/mysql:/bin/bash
[root@DB-Server ~]# more /etc/shadow | grep mysql
mysql:!!:16496::::::
[root@DB-Server ~]# more /etc/group | grep mysql
mysql:x:501:
[root@DB-Server ~]# userdel mysql
[root@DB-Server ~]# groupdel mysql
groupdel: group mysql does not exist
[root@DB-Server ~]# 


7：确认MySQL是否卸载删除

[root@DB-Server init.d]# rpm -qa | grep -i mysql

 

二进制包/源码安装方式的MySQL卸载

如果是采用二进制包安装的MySQL，那么你用下面命令是找不到任何MySQL组件的。所以如果你不知道MySQL的安装方式，千万不要用下面命令来判别是否安装了MySQL

[root@DB-Server init.d]# rpm -qa | grep -i mysql

 

- 检查MySQL服务并关闭服务进程。

 

首先通过进程查看是否有MySQL的服务的状态, 如下所示，MySQL服务是启动的。

[root@DB-Server init.d]# ps -ef | grep mysql
root      4752  4302  0 22:55 pts/1    00:00:00 more /etc/init.d/mysql.server
root      7176     1  0 23:23 pts/1    00:00:00 /bin/sh /usr/local/mysql/bin/mysqld_safe --datadir=/usr/local/mysql/data --pid-file=/usr/local/mysql/data/DB-Server.localdomain.pid
mysql     7269  7176 15 23:23 pts/1    00:00:01 /usr/local/mysql/bin/mysqld --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data --plugin-dir=/usr/local/mysql/lib/plugin --user=mysql --log-error=/usr/local/mysql/data/DB-Server.localdomain.err --pid-file=/usr/local/mysql/data/DB-Server.localdomain.pid
root      7321  4302  0 23:23 pts/1    00:00:00 grep mysql
[root@DB-Server init.d]# /etc/init.d/mysql.server status
MySQL running (7269)[  OK  ]
[root@DB-Server init.d]# /etc/init.d/mysql.server stop
Shutting down MySQL..[  OK  ]
[root@DB-Server init.d]# /etc/init.d/mysql.server status
MySQL is not running[FAILED]
[root@DB-Server init.d]# 
![](https://github.com/zkydrx/images/blob/master/sql/6.png?raw=true)

 

- 查找MySQL的安装目录并彻底删除

[root@DB-Server init.d]# whereis mysql

mysql: /usr/local/mysql

[root@DB-Server init.d]# find / -name mysql

/var/spool/mail/mysql

/usr/local/mysql-5.7.5-m15-linux-glibc2.5-x86_64/include/mysql

/usr/local/mysql-5.7.5-m15-linux-glibc2.5-x86_64/bin/mysql

/usr/local/mysql-5.7.5-m15-linux-glibc2.5-x86_64/data/mysql

/usr/local/mysql

![](https://github.com/zkydrx/images/blob/master/sql/7.png?raw=true)

[root@DB-Server init.d]# rm -rf /usr/local/mysql-5.7.5-m15-linux-glibc2.5-x86_64/

[root@DB-Server init.d]# rm -rf /usr/local/

[root@DB-Server init.d]# rm -rf /var/spool/mail/mysql

[root@DB-Server init.d]# 

 

- 删除一些配置文件

配置文件一般有/etc/my.cnf 或/etc/init.d/mysql.server，视具体安装配置情况而定。

 

- 删除MySQL用户以及用户组

[root@DB-Server ~]# id mysql

uid=101(mysql) gid=501(mysql) groups=501(mysql) context=root:system_r:unconfined_t:SystemLow-SystemHigh

[root@DB-Server ~]# userdel mysql

 