**前提：必须正确安装JDK**

**一、通过二进制包（tar.gz）安装**

**下载：**

[https://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-8/v8.5.16/bin/](https://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-8/v8.5.16/bin/)

如果是在命令行下，推荐使用links，如下所示：

**安装步骤：**

解压

tar zxvf apache-tomcat-8.5.16.tar.gz

移动

sudo mv apache-tomcat-8.5.16//opt/apache-tomcat-8.5.16

创建链接

sudo ln -s /opt/apache-tomcat-8.5.16//opt/tomcat8

启动

/opt/tomcat8/bin/startup.sh

访问测试

http://127.0.0.1:8080/

配置管理员权限

sudo vim/opt/tomcat8/conf/tomcat-users.xml

<rolerolename="manager-gui"/> <rolerolename="admin-gui"/> <user username="root"password="123456" roles="manager-gui,admin-gui"/>

提示：按“i”插入，按Exc之后输入“：wq！”保存。

重启

/opt/tomcat8/bin/shutdown.sh/opt/tomcat8/bin/startup.sh

注册成系统服务，开机自动启动

sudo vim /opt/tomcat8/bin/catalina.sh

\#假设配置了JAVA_HOME变量和TOMCAT_HOME变量CATALINA_HOME=$TOMCAT_HOME CLASSPATH=.:$JAVA_HOME/lib:$CATALINA_HOME/lib #如果都没有配置 JAVA_HOME=/usr/lib/jvm/java-8-oracle CATALINA_HOME=/opt/tomcat8CLASSPATH=.:$JAVA_HOME/lib:$CATALINA_HOME/lib

sudo cp /opt/tomcat8/bin/catalina.sh/etc/init.d/tomcat8

sudo sysv-rc-conf

其实运行级别在2就行了，不用全部，全部只是处于保险。

完成后按Q退出，然后重启测试效果。

**二、通过****APT****源安装**

安装：

sudo apt-get install tomcat8tomcat8-docs tomcat8-examples tomcat8-admin

安装完成后的配置文件放置在/var/lib/。

服务启动：

\#启动 servicetomcat8 start #状态 servicetomcat8 status #停止 service tomcat8 stop

配置管理员权限：

sudo vim/var/lib/tomcat8/conf/tomcat-users.xml

<rolerolename="manager-gui"/> 

<rolerolename="admin-gui"/> 

<user username="root"password="123456" roles="manager-gui,admin-gui"/>

提示：按“i”插入，按Exc之后输入“：wq！”保存。

重启服务测试：

sudo service tomcat8 restart

http://127.0.0.1:8080/

配置服务自启动：

sudo sysv-rc-conf

其实运行级别在2就行了，不用全部，全部只是处于保险。

卸载：

sudo apt-get autoremove tomcat8

 

参考：

[http://blog.sina.com.cn/s/blog_484d87770102uxz6.html](http://blog.sina.com.cn/s/blog_484d87770102uxz6.html)

[http://blog.csdn.net/efregrh/article/details/52903673](http://blog.csdn.net/efregrh/article/details/52903673)

[http://www.jb51.net/article/95273.htm](http://www.jb51.net/article/95273.htm)

经过检验 可行。

 