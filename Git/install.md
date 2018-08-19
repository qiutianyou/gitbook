# Git 安装
这里就不记录Windows/Mac OS系统的了，直接下载对应的安装程序，按步骤安装即可。
##### Linux 安装
登陆https://git-scm.com/download/linux

<b>源码安装</b>
#### 1. 下载源码
可以在另一台电脑中下载好源码，然后上传至Linux服务器
https://mirrors.edge.kernel.org/pub/software/scm/git/
找到对应的版本。
#### 2. 上传至服务器
以git-2.9.5.tar.gz为例，将下载好的文件上传至服务器。
``` Linux
scp git-2.9.5.tar.gz  root@192.168.0.102:/home/tools   
```

  scp git-2.9.5.tar.gz 目标机器的用户@目标机器ip:目标机器路径
#### 3. 解压并安装
登陆目标机器，解压并安装。/home/Git是指的安装目录

 ``` Linux
tar -zxvf git-manpages-2.9.5.tar.gz
cd git-2.9.5
[root@localhost git-2.9.5]# ./configure  --prefix=/home/Git
[root@localhost git-2.9.5]# make && make install
 ```


#### 4. ./configure 报错
``` Linux
[root@localhost git-2.9.5]# ./configure  --prefix=/home/Git
configure: Setting lib to 'lib' (the default)
configure: Will try -pthread then -lpthread to enable POSIX Threads.
configure: CHECKS for site configuration
checking for gcc... no
checking for cc... no
checking for cl.exe... no
configure: error: in `/home/tools/git-2.9.5':
configure: error: no acceptable C compiler found in $PATH
See `config.log' for more details
```
我的linux服务器执行报错中看出，gcc,cc,cl.exe为no。gcc是Linux的c语言编译器，说明我的机器中没有安装这些编译器。
分别安装以下gcc,gcc-c++,安装成功之后在执行一下git的安装命令
  ``` Linux
  [root@localhost git-2.9.5]# yum install gcc
  [root@localhost git-2.9.5]# yum install gcc-c++
  [root@localhost git-2.9.5]# ./configure  --prefix=/home/Git
  ```
#### 5. make命令报错
``` linux
[root@localhost git-2.9.5]# make && make install
    * new build flags
    CC credential-store.o
In file included from credential-store.c:1:0:
cache.h:40:18: 致命错误：zlib.h：没有那个文件或目录
 #include <zlib.h>
                  ^
编译中断。
make: *** [credential-store.o] 错误 1
```

缺少 zlib的头文件， 开发包没装。
* 安装zlib
  ``` Linux
  [root@localhost git-2.9.5]# yum install zlib
  [root@localhost git-2.9.5]# yum install zlib-devel
  [root@localhost git-2.9.5]# yum install perl-ExtUtils-CBuilder perl-ExtUtils-MakeMaker
  [root@localhost git-2.9.5]# make && make install
  ```
  若无报错则安装成功

#### 6.检查git安装是否完成
进入之前指定的安装目录，查看git版本，能成功则表示git安装完成
``` Linux
[root@localhost bin]# cd /home/Git/bin
[root@localhost bin]# ./git --version
git version 2.9.5
```

#### 7.配置环境变量

``` Linux
vi /etc/profile
```
编辑环境变量配置文件，在最后追加下面的字符串，指定bin目录的地址
export PATH=$PATH://home/Git/bin

修改完成之后，执行命令，生效配置文件
``` linux
source /etc/profile
```
检查是否配置成功，可切换路径到其他目录中，执行 git --version。返回git版本则表示环境变量配置完成。

#### 8.fatal: Unable to find remote helper for 'https'
如果出现clone报错的问题。
``` linux
yum install curl-devel
cd /home/tools/git-2.9.5/
./configure
make
make install
```
再次尝试一下clone。不行则重启一下
``` linux
reboot
```
