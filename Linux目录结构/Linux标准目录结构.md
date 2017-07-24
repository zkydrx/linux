## **Linux 目录结构**

初学[Linux](http://lib.csdn.net/base/linux)，首先需要弄清[linux](http://lib.csdn.net/base/linux) 标准目录结构

![](https://github.com/zkydrx/images/blob/master/linux/linux.png?raw=true)

- root --- 启动[Linux](http://linux-wiki.cn/wiki/Linux)时使用的一些核心文件。如操作系统[内核](http://linux-wiki.cn/index.php?title=%E5%86%85%E6%A0%B8&action=edit&redlink=1)、引导程序[Grub](http://linux-wiki.cn/wiki/Category:Grub)等。

- home --- 

  存储普通用户的个人文件

  - ftp --- 用户所有服务
  - httpd
  - samba
  - user1
  - user2

- bin --- 系统启动时需要的执行文件（二进制）

- sbin --- 可执行程序的目录，但大多存放涉及系统管理的命令。只有root权限才能执行

- proc --- 虚拟，存在linux内核镜像；保存所有内核参数以及系统配置信息

  - 1 --- 进程编号

- usr --- 用户目录，存放

  用户级的文件

  - bin --- 几乎所有用户所用命令，另外存在与/bin，/usr/local/bin
  - sbin --- 系统管理员命令，与用户相关，例如，大部分服务器程序
  - include ---  存放C/C++头文件的目录
  - lib --- 固定的程序数据
  - local --- 本地安装软件保存位置
  - man --- 手工生成的目录
  - info --- 信息文档
  - doc --- 不同包文档信息
  - tmp
  - X11R6 ---  该目录用于保存运行X-Window所需的所有文件。该目录中还包含用于运行GUI要的配置文件和二进制文件。
  - X386　--- 功能同X11R6，X11 发行版5 的系统文件

- boot --- 引导加载器所需文件，系统所需图片保存于此

- lib --- 

  根文件系统目录下程序和核心模块的

  公共库

  - modules --- 可加载模块，系统崩溃后重启所需模块

- dev --- 设备文件目录

- etc --- 配置文件

  - skel --- home目录建立，该目录初始化
  - sysconfig --- 网络，时间，键盘等配置目录

- var

  - file
  - lib --- 该目录下的文件在系统运行时，会改变
  - local --- 安装在/usr/local的程序数据，变化的
  - lock --- 文件使用特定外设或文件，为其上锁，其他文件暂时不能访问
  - log --- 记录日志
  - run --- 系统运行合法信息
  - spool --- 打印机、邮件、代理服务器等假脱机目录
  - tmp
  - catman --- 缓存目录

- mnt --- 临时用于挂载文件系统的地方。一般情况下这个目录是空的，而在我们将要挂载分区时在这个目录下建立目录，再将我们将要访问的设备[挂载](http://linux-wiki.cn/wiki/Category:Mount)在这个目录上，这样我们就可访问文件了。

- tmp --- 临时文件目录，系统启动后的临时文件存放在/var/tmp

- lost+found --- 在文件系统修复时恢复的文件

 

/：根目录，一般根目录下只存放目录，不要存放文件，/etc、/bin、/dev、/lib、/sbin应该和根目录放置在一个分区中

/bin:/usr/bin:可执行二进制文件的目录，如常用的命令ls、tar、mv、cat等。

/boot：放置linux系统启动时用到的一些文件。/boot/vmlinuz为linux的内核文件，以及/boot/gurb。建议单独分区，分区大小100M即可

/dev：存放linux系统下的设备文件，访问该目录下某个文件，相当于访问某个设备，常用的是挂载光驱mount /dev/cdrom /mnt。

/etc：系统配置文件存放的目录，不建议在此目录下存放可执行文件，重要的配置文件有/etc/inittab、/etc/fstab、/etc/init.d、/etc/X11、/etc/sysconfig、/etc/xinetd.d修改配置文件之前记得备份。

注：/etc/X11存放与x windows有关的设置。

/home：系统默认的用户家目录，新增用户账号时，用户的家目录都存放在此目录下，~表示当前用户的家目录，~test表示用户test的家目录。建议单独分区，并设置较大的磁盘空间，方便用户存放数据

/lib:/usr/lib:/usr/local/lib：系统使用的函数库的目录，程序在执行过程中，需要调用一些额外的参数时需要函数库的协助，比较重要的目录为/lib/modules。

/lost+fount：系统异常产生错误时，会将一些遗失的片段放置于此目录下，通常这个目录会自动出现在装置目录下。如加载硬盘于/disk 中，此目录下就会自动产生目录/disk/lost+found

/mnt:/media：光盘默认挂载点，通常光盘挂载于/mnt/cdrom下，也不一定，可以选择任意位置进行挂载。

/opt：给主机额外安装软件所摆放的目录。如：FC4使用的Fedora 社群开发软件，如果想要自行安装新的KDE 桌面软件，可以将该软件安装在该目录下。以前的 Linux 系统中，习惯放置在 /usr/local 目录下

/proc：此目录的数据都在内存中，如系统核心，外部设备，网络状态，由于数据都存放于内存中，所以不占用磁盘空间，比较重要的目录有/proc/cpuinfo、/proc/interrupts、/proc/dma、/proc/ioports、/proc/net/*等

/root：系统管理员root的家目录，系统第一个启动的分区为/，所以最好将/root和/放置在一个分区下。

/sbin:/usr/sbin:/usr/local/sbin：放置系统管理员使用的可执行命令，如fdisk、shutdown、mount等。与/bin不同的是，这几个目录是给系统管理员root使用的命令，一般用户只能"查看"而不能设置和使用。

/tmp：一般用户或正在执行的程序临时存放文件的目录,任何人都可以访问,重要数据不可放置在此目录下

/srv：服务启动之后需要访问的数据目录，如www服务需要访问的网页数据存放在/srv/www内

/usr：应用程序存放目录，/usr/bin存放应用程序，/usr/share存放共享数据，/usr/lib存放不能直接运行的，却是许多程序运行所必需的一些函数库文件。/usr/local:存放软件升级包。/usr/share/doc:系统说明文件存放目录。/usr/share/man: 程序说明文件存放目录，使用 man ls时会查询/usr/share/man/man1/ls.1.gz的内容建议单独分区，设置较大的磁盘空间

/var：放置系统执行过程中经常变化的文件，如随时更改的日志文件/var/log，/var/log/message：所有的登录文件存放目录，/var/spool/mail：邮件存放的目录，/var/run:程序或服务启动后，其PID存放在该目录下。建议单独分区，设置较大的磁盘空间

**常用指令**

ls　　        显示文件或目录

​     -l           列出文件详细信息l(list)

​     -a          列出当前目录下所有文件及目录，包括隐藏的a(all)

mkdir         创建目录

​     -p           创建目录，若无父目录，则创建p(parent)

cd               切换目录

touch          创建空文件

echo            创建带有内容的文件。

cat              查看文件内容

cp                拷贝

mv               移动或重命名

rm               删除文件

​     -r            递归删除，可删除子目录及文件

​     -f            强制删除

find              在文件系统中搜索某文件

wc                统计文本中行数、字数、字符数

grep             在文本文件中查找某个字符串

rmdir           删除空目录

tree             树形结构显示目录，需要安装tree包

pwd              显示当前目录

ln                  创建链接文件

more、less  分页显示文本文件内容

head、tail    显示文件头、尾内容

ctrl+alt+F1  命令行全屏模式

**系统管理命令**

stat              显示指定文件的详细信息，比ls更详细

who               显示在线登陆用户

whoami          显示当前操作用户

hostname      显示主机名

uname           显示系统信息

top                动态显示当前耗费资源最多进程信息

ps                  显示瞬间进程状态 ps -aux

du                  查看目录大小 du -h /home带有单位显示目录信息

df                  查看磁盘大小 df -h 带有单位显示磁盘信息

ifconfig          查看网络情况

ping                [测试](http://lib.csdn.net/base/softwaretest)网络连通

netstat          显示网络状态信息

man                命令不会用了，找男人  如：man ls

clear              清屏

alias               对命令重命名 如：alias showmeit="ps -aux" ，另外解除使用unaliax showmeit

kill                 杀死进程，可以先用ps 或 top命令查看进程的id，然后再用kill命令杀死进程。

**打包压缩相关命令**

gzip：

bzip2：

tar:                打包压缩

​     -c              归档文件

​     -x              压缩文件

​     -z              gzip压缩文件

​     -j              bzip2压缩文件

​     -v              显示压缩或解压缩过程 v(view)

​     -f              使用档名

例：

tar -cvf /home/abc.tar /home/abc              只打包，不压缩

tar -zcvf /home/abc.tar.gz /home/abc        打包，并用gzip压缩

tar -jcvf /home/abc.tar.bz2 /home/abc      打包，并用bzip2压缩

当然，如果想解压缩，就直接替换上面的命令  tar -cvf  / tar -zcvf  / tar -jcvf 中的“c” 换成“x” 就可以了。

**关机/重启机器**

shutdown

​     -r             关机重启

​     -h             关机不重启

​     now          立刻关机

halt               关机

reboot          重启

**Linux管道**

将一个命令的标准输出作为另一个命令的标准输入。也就是把几个命令组合起来使用，

```
就是把前一个命令的结果当成后一个命令的输入。
```

例：grep -r "close" /home/* | more       在home目录下所有文件中查找，包括close的文件，并分页输出。

**Linux软件包管理**

**dpkg** (Debian Package)管理工具，软件包名以.deb后缀。这种方法适合系统不能联网的情况下。

比如安装tree命令的安装包，先将tree.deb传到Linux系统中。再使用如下命令安装。

sudo dpkg -i tree_1.5.3-1_i386.deb         安装软件

sudo dpkg -r tree                                     卸载软件

 

注：将tree.deb传到Linux系统中，有多种方式。VMwareTool，使用挂载方式；使用winSCP工具等；

**APT**（Advanced Packaging Tool）高级软件工具。这种方法适合系统能够连接互联网的情况。

依然以tree为例

sudo apt-get install tree                         安装tree

sudo apt-get remove tree                       卸载tree

sudo apt-get update                                 更新软件

sudo apt-get upgrade        

 

将.**rpm**文件转为.**deb**文件

.rpm为RedHat使用的软件格式。在Ubuntu下不能直接使用，所以需要转换一下。

sudo alien abc.rpm

 

**vim使用**

vim三种模式：命令模式、插入模式、编辑模式。使用ESC或i或：来切换模式。

命令模式下：

:q                      退出

:q!                     强制退出

:wq                   保存并退出

:set number     显示行号

:set nonumber  隐藏行号

/apache            在文档中查找apache 按n跳到下一个，shift+n上一个

yyp                   复制光标所在行，并粘贴

h(左移一个字符←)、j(下一行↓)、k(上一行↑)、l(右移一个字符→)

 

**用户及用户组管理**

/etc/passwd    存储用户账号

/etc/group       存储组账号

/etc/shadow    存储用户账号的密码

/etc/gshadow  存储用户组账号的密码

useradd 用户名

userdel 用户名

adduser 用户名

groupadd 组名

groupdel 组名

passwd root     给root设置密码

su root

su - root 

/etc/profile     系统环境变量

bash_profile     用户环境变量

.bashrc              用户环境变量

su user              切换用户，加载配置文件.bashrc

su - user            切换用户，加载配置文件/etc/profile ，加载bash_profile

**更改文件的用户及用户组**

sudo chown [-R] owner[:group] {File|Directory}

例如：还以jdk-7u21-linux-i586.tar.gz为例。属于用户[Hadoop](http://lib.csdn.net/base/hadoop)，组[hadoop](http://lib.csdn.net/base/hadoop)

要想切换此文件所属的用户及组。可以使用命令。

sudo chown root:root jdk-7u21-linux-i586.tar.gz

 

**文件权限管理**

三种基本权限

R           读         数值表示为4

W          写         数值表示为2

X           可执行  数值表示为1

如图所示，zhangjunzhao文件的权限为drwxr-xr-x

drwxr-xr-x一共十个字符，分成四段。

第一个字符“-”表示普通文件；这个位置还可能会出现“l”链接；“d”表示目录

第二三四个字符“rwx”表示当前所属用户的权限。   所以用数值表示为4+2+1=7

第五六七个字符“r-x”表示当前所属组的权限。      所以用数值表示为4+1=5

第八九十个字符“r-x”表示其他用户权限。              所以用数值表示为4+1=5

所以操作此文件的权限用数值表示为755 

**更改权限**

sudo chmod [u所属用户  g所属组  o其他用户  a所有用户]  [+增加权限  -减少权限]  [r  w  x]   目录名 

例如：有一个文件filename，权限为“-rw-r----x” ,将权限值改为"-rwxrw-r-x"，用数值表示为765

sudo chmod u+x g+w o+r  filename

上面的例子可以用数值表示

sudo chmod 765 filename