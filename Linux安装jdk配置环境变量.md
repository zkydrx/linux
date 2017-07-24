作为一个Linux新手，在写这篇文章之前，安装了几次jdk，好多次都是环境变量配置错误，导致无法登录系统。经过几天的研究，今天新装系统，从头来完整配置一遍

系统版本：[Ubuntu](http://www.linuxidc.com/topicnews.aspx?tid=2) 16.04

JDK版本：jdk1.8.0_121

1.官网下载JDK文件jdk-8u121-linux-x64.tar.gz

我这里下的是最新版，其他版本也可以

2.创建一个目录作为JDK的安装目录，我的目录为 /java

sudomkdir /java

![](https://github.com/zkydrx/images/blob/master/linux/1.png?raw=true)

3.移动文件到/java目录下

sudo mvjdk-8u121-linux-x64.tar.gz /java

![](https://github.com/zkydrx/images/blob/master/linux/2.png?raw=true)

4.解压文件

tar-zxvf jdk-8u121-linux-x64.tar.gz

5.配置环境变量

sudogedit /etc/environment

末尾加入以下配置（JAVA_HOME后的路径就是jdk的文件位置）

PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:$JAVA_HOME/bin"
export CLASSPATH=.:$JAVA_HOME/lib:$JAVA_HOME/jre/lib
export JAVA_HOME=/java/jdk1.8.0_121

修改完成之后保存关闭，并输入以下命令使环境变量立即生效

source/etc/environment

6.输入java-version，显示JDK版本说明恭喜你，环境变量配置正确

![](https://github.com/zkydrx/images/blob/master/linux/3.png?raw=true)

7.但还没结束，以前按照其他人写的文章发现每次重启后就用不了了，所以还需要**配置所有用户的环境变量**

sudogedit /etc/profile

在文件的最后添加以下内容：

\#setJava environment

export
JAVA_HOME=/dengyang/jdk1.8.0_56
export JRE_HOME=$JAVA_HOME/jre
export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib:$CLASSPATH
export PATH=$JAVA_HOME/bin:$JRE_HOME/bin:$PATH

8.同样，需要使用命令使环境变量立即生效

source/etc/profile

9.重启电脑，能正常进入系统，且java-version命令有效

 