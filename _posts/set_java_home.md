# Centos设置java_home

```shell
[root@hadoop001 schema]# which java
/usr/bin/java
[root@hadoop001 schema]# ls -lr /usr/bin/java
lrwxrwxrwx 1 root root 22 9月  10 2018 /usr/bin/java -> /etc/alternatives/java
[root@hadoop001 schema]# ls -lrt /etc/alternatives/java
lrwxrwxrwx 1 root root 41 9月  10 2018 /etc/alternatives/java -> /usr/java/jdk1.8.0_181-amd64/jre/bin/java

#/usr/java/jdk1.8.0_181-amd64/就是jdk的路径
#打开 /etc/profile
#在结尾处输入 
export JAVA_HOME=/usr/java/jdk1.8.0_181-amd64/
export JRE_HOME=$JAVA_HOME/jre
#export CLASSPATH=$JAVA_HOME/lib:$JRE_HOME/lib:$CLASSPATH
export PATH=$JAVA_HOME/bin:$JRE_HOME/bin:$PATH

```
#mount nas的共享路径
```shell
mount -t cifs -o username=admin,pass=jjjkkk12 //192.168.1.108/Download /mnt
```
安装 cloudera-daemons

```shell
[root@hadoop001 cdh]# yum install cloudera-manager-daemons-6.3.0-1281944.el7.x86_64.rpm 
已加载插件：fastestmirror, langpacks
正在检查 cloudera-manager-daemons-6.3.0-1281944.el7.x86_64.rpm: cloudera-manager-daemons-6.3.0-1281944.el7.x86_64
cloudera-manager-daemons-6.3.0-1281944.el7.x86_64.rpm 将被安装
正在解决依赖关系
--> 正在检查事务
---> 软件包 cloudera-manager-daemons.x86_64.0.6.3.0-1281944.el7 将被 安装
--> 解决依赖关系完成
base/7/x86_64                                                                                                                                       | 3.6 kB  00:00:00     
base/7/x86_64/group_gz                                                                                                                              | 166 kB  00:00:00     
base/7/x86_64/primary_db                                                                                                                            | 6.0 MB  00:00:00     
extras/7/x86_64                                                                                                                                     | 3.4 kB  00:00:00     
extras/7/x86_64/primary_db                                                                                                                          | 215 kB  00:00:00     
updates/7/x86_64                                                                                                                                    | 3.4 kB  00:00:00     
updates/7/x86_64/primary_db                                                                                                                         | 7.4 MB  00:00:00     

依赖关系解决

===========================================================================================================================================================================
 Package                                 架构                  版本                                源                                                                 大小
===========================================================================================================================================================================
正在安装:
 cloudera-manager-daemons                x86_64                6.3.0-1281944.el7                   /cloudera-manager-daemons-6.3.0-1281944.el7.x86_64                1.3 G

事务概要
===========================================================================================================================================================================
安装  1 软件包

总计：1.3 G
安装大小：1.3 G
Is this ok [y/d/N]: y
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  正在安装    : cloudera-manager-daemons-6.3.0-1281944.el7.x86_64                                                                                                      1/1 
  验证中      : cloudera-manager-daemons-6.3.0-1281944.el7.x86_64                                                                                                      1/1 

已安装:
  cloudera-manager-daemons.x86_64 0:6.3.0-1281944.el7                                                                                                                      

完毕！


```

安装cloudera manager

```shell
[root@hadoop001 cdh]# yum install cloudera-manager-server-6.3.0-1281944.el7.x86_64.rpm
已加载插件：fastestmirror, langpacks
正在检查 cloudera-manager-server-6.3.0-1281944.el7.x86_64.rpm: cloudera-manager-server-6.3.0-1281944.el7.x86_64
cloudera-manager-server-6.3.0-1281944.el7.x86_64.rpm 将被安装
正在解决依赖关系
--> 正在检查事务
---> 软件包 cloudera-manager-server.x86_64.0.6.3.0-1281944.el7 将被 安装
--> 解决依赖关系完成

依赖关系解决

===========================================================================================================================================================================
 Package                                 架构                   版本                               源                                                                 大小
===========================================================================================================================================================================
正在安装:
 cloudera-manager-server                 x86_64                 6.3.0-1281944.el7                  /cloudera-manager-server-6.3.0-1281944.el7.x86_64                  14 k

事务概要
===========================================================================================================================================================================
安装  1 软件包

总计：14 k
安装大小：14 k
Is this ok [y/d/N]: y
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  正在安装    : cloudera-manager-server-6.3.0-1281944.el7.x86_64                                                                                                       1/1 
Created symlink from /etc/systemd/system/multi-user.target.wants/cloudera-scm-server.service to /usr/lib/systemd/system/cloudera-scm-server.service.
  验证中      : cloudera-manager-server-6.3.0-1281944.el7.x86_64                                                                                                       1/1 

已安装:
  cloudera-manager-server.x86_64 0:6.3.0-1281944.el7                                                                                                                       

完毕！
```
安装cloudera agent

```shell

[root@hadoop001 cdh]# yum install cloudera-manager-agent-6.3.0-1281944.el7.x86_64.rpm 
已加载插件：fastestmirror, langpacks
正在检查 cloudera-manager-agent-6.3.0-1281944.el7.x86_64.rpm: cloudera-manager-agent-6.3.0-1281944.el7.x86_64
cloudera-manager-agent-6.3.0-1281944.el7.x86_64.rpm 将被安装
正在解决依赖关系
--> 正在检查事务
---> 软件包 cloudera-manager-agent.x86_64.0.6.3.0-1281944.el7 将被 安装
--> 正在处理依赖关系 psmisc，它被软件包 cloudera-manager-agent-6.3.0-1281944.el7.x86_64 需要
Loading mirror speeds from cached hostfile
 * base: mirror.jdcloud.com
 * extras: mirror.jdcloud.com
 * updates: ap.stykers.moe
--> 正在处理依赖关系 cyrus-sasl-gssapi，它被软件包 cloudera-manager-agent-6.3.0-1281944.el7.x86_64 需要
--> 正在处理依赖关系 fuse，它被软件包 cloudera-manager-agent-6.3.0-1281944.el7.x86_64 需要
--> 正在处理依赖关系 fuse-libs，它被软件包 cloudera-manager-agent-6.3.0-1281944.el7.x86_64 需要
--> 正在处理依赖关系 /lib/lsb/init-functions，它被软件包 cloudera-manager-agent-6.3.0-1281944.el7.x86_64 需要
base/7/x86_64/filelists_db                                                                                                                          | 7.1 MB  00:00:02     
extras/7/x86_64/filelists_db                                                                                                                        | 249 kB  00:00:00     
updates/7/x86_64/filelists_db                                                                                                                       | 5.2 MB  00:00:01     
--> 正在处理依赖关系 httpd，它被软件包 cloudera-manager-agent-6.3.0-1281944.el7.x86_64 需要
--> 正在处理依赖关系 mod_ssl，它被软件包 cloudera-manager-agent-6.3.0-1281944.el7.x86_64 需要
--> 正在处理依赖关系 openssl-devel，它被软件包 cloudera-manager-agent-6.3.0-1281944.el7.x86_64 需要
--> 正在处理依赖关系 python-psycopg2，它被软件包 cloudera-manager-agent-6.3.0-1281944.el7.x86_64 需要
--> 正在处理依赖关系 MySQL-python，它被软件包 cloudera-manager-agent-6.3.0-1281944.el7.x86_64 需要
--> 正在处理依赖关系 libpq.so.5()(64bit)，它被软件包 cloudera-manager-agent-6.3.0-1281944.el7.x86_64 需要
--> 正在检查事务
---> 软件包 MySQL-python.x86_64.0.1.2.5-1.el7 将被 安装
---> 软件包 cyrus-sasl-gssapi.x86_64.0.2.1.26-23.el7 将被 安装
---> 软件包 fuse.x86_64.0.2.9.2-11.el7 将被 安装
---> 软件包 fuse-libs.x86_64.0.2.9.2-11.el7 将被 安装
---> 软件包 httpd.x86_64.0.2.4.6-89.el7.centos.1 将被 安装
--> 正在处理依赖关系 httpd-tools = 2.4.6-89.el7.centos.1，它被软件包 httpd-2.4.6-89.el7.centos.1.x86_64 需要
--> 正在处理依赖关系 /etc/mime.types，它被软件包 httpd-2.4.6-89.el7.centos.1.x86_64 需要
---> 软件包 mod_ssl.x86_64.1.2.4.6-89.el7.centos.1 将被 安装
---> 软件包 openssl-devel.x86_64.1.1.0.2k-16.el7_6.1 将被 安装
--> 正在处理依赖关系 openssl-libs(x86-64) = 1:1.0.2k-16.el7_6.1，它被软件包 1:openssl-devel-1.0.2k-16.el7_6.1.x86_64 需要
--> 正在处理依赖关系 zlib-devel(x86-64)，它被软件包 1:openssl-devel-1.0.2k-16.el7_6.1.x86_64 需要
--> 正在处理依赖关系 krb5-devel(x86-64)，它被软件包 1:openssl-devel-1.0.2k-16.el7_6.1.x86_64 需要
---> 软件包 postgresql-libs.x86_64.0.9.2.24-1.el7_5 将被 安装
---> 软件包 psmisc.x86_64.0.22.20-15.el7 将被 安装
---> 软件包 python-psycopg2.x86_64.0.2.5.1-3.el7 将被 安装
---> 软件包 redhat-lsb-core.x86_64.0.4.1-27.el7.centos.1 将被 安装
--> 正在处理依赖关系 redhat-lsb-submod-security(x86-64) = 4.1-27.el7.centos.1，它被软件包 redhat-lsb-core-4.1-27.el7.centos.1.x86_64 需要
--> 正在处理依赖关系 spax，它被软件包 redhat-lsb-core-4.1-27.el7.centos.1.x86_64 需要
--> 正在处理依赖关系 /usr/bin/lpr，它被软件包 redhat-lsb-core-4.1-27.el7.centos.1.x86_64 需要
--> 正在处理依赖关系 /usr/bin/lp，它被软件包 redhat-lsb-core-4.1-27.el7.centos.1.x86_64 需要
--> 正在检查事务
---> 软件包 cups-client.x86_64.1.1.6.3-35.el7 将被 安装
--> 正在处理依赖关系 cups-libs(x86-64) = 1:1.6.3-35.el7，它被软件包 1:cups-client-1.6.3-35.el7.x86_64 需要
--> 正在处理依赖关系 libcups.so.2()(64bit)，它被软件包 1:cups-client-1.6.3-35.el7.x86_64 需要
---> 软件包 httpd-tools.x86_64.0.2.4.6-89.el7.centos.1 将被 安装
---> 软件包 krb5-devel.x86_64.0.1.15.1-37.el7_6 将被 安装
--> 正在处理依赖关系 libkadm5(x86-64) = 1.15.1-37.el7_6，它被软件包 krb5-devel-1.15.1-37.el7_6.x86_64 需要
--> 正在处理依赖关系 krb5-libs(x86-64) = 1.15.1-37.el7_6，它被软件包 krb5-devel-1.15.1-37.el7_6.x86_64 需要
--> 正在处理依赖关系 libverto-devel，它被软件包 krb5-devel-1.15.1-37.el7_6.x86_64 需要
--> 正在处理依赖关系 libselinux-devel，它被软件包 krb5-devel-1.15.1-37.el7_6.x86_64 需要
--> 正在处理依赖关系 libcom_err-devel，它被软件包 krb5-devel-1.15.1-37.el7_6.x86_64 需要
--> 正在处理依赖关系 keyutils-libs-devel，它被软件包 krb5-devel-1.15.1-37.el7_6.x86_64 需要
---> 软件包 mailcap.noarch.0.2.1.41-2.el7 将被 安装
---> 软件包 openssl-libs.x86_64.1.1.0.2k-12.el7 将被 升级
--> 正在处理依赖关系 openssl-libs(x86-64) = 1:1.0.2k-12.el7，它被软件包 1:openssl-1.0.2k-12.el7.x86_64 需要
---> 软件包 openssl-libs.x86_64.1.1.0.2k-16.el7_6.1 将被 更新
---> 软件包 redhat-lsb-submod-security.x86_64.0.4.1-27.el7.centos.1 将被 安装
---> 软件包 spax.x86_64.0.1.5.2-13.el7 将被 安装
---> 软件包 zlib-devel.x86_64.0.1.2.7-18.el7 将被 安装
--> 正在处理依赖关系 zlib = 1.2.7-18.el7，它被软件包 zlib-devel-1.2.7-18.el7.x86_64 需要
--> 正在检查事务
---> 软件包 cups-libs.x86_64.1.1.6.3-35.el7 将被 安装
---> 软件包 keyutils-libs-devel.x86_64.0.1.5.8-3.el7 将被 安装
---> 软件包 krb5-libs.x86_64.0.1.15.1-19.el7 将被 升级
---> 软件包 krb5-libs.x86_64.0.1.15.1-37.el7_6 将被 更新
---> 软件包 libcom_err-devel.x86_64.0.1.42.9-13.el7 将被 安装
--> 正在处理依赖关系 libcom_err(x86-64) = 1.42.9-13.el7，它被软件包 libcom_err-devel-1.42.9-13.el7.x86_64 需要
---> 软件包 libkadm5.x86_64.0.1.15.1-37.el7_6 将被 安装
---> 软件包 libselinux-devel.x86_64.0.2.5-14.1.el7 将被 安装
--> 正在处理依赖关系 libselinux(x86-64) = 2.5-14.1.el7，它被软件包 libselinux-devel-2.5-14.1.el7.x86_64 需要
--> 正在处理依赖关系 libsepol-devel(x86-64) >= 2.5-10，它被软件包 libselinux-devel-2.5-14.1.el7.x86_64 需要
--> 正在处理依赖关系 pkgconfig(libsepol)，它被软件包 libselinux-devel-2.5-14.1.el7.x86_64 需要
--> 正在处理依赖关系 pkgconfig(libpcre)，它被软件包 libselinux-devel-2.5-14.1.el7.x86_64 需要
---> 软件包 libverto-devel.x86_64.0.0.2.5-4.el7 将被 安装
---> 软件包 openssl.x86_64.1.1.0.2k-12.el7 将被 升级
---> 软件包 openssl.x86_64.1.1.0.2k-16.el7_6.1 将被 更新
---> 软件包 zlib.i686.0.1.2.7-17.el7 将被 升级
---> 软件包 zlib.x86_64.0.1.2.7-17.el7 将被 升级
---> 软件包 zlib.i686.0.1.2.7-18.el7 将被 更新
---> 软件包 zlib.x86_64.0.1.2.7-18.el7 将被 更新
--> 正在检查事务
---> 软件包 libcom_err.x86_64.0.1.42.9-12.el7_5 将被 升级
--> 正在处理依赖关系 libcom_err(x86-64) = 1.42.9-12.el7_5，它被软件包 libss-1.42.9-12.el7_5.x86_64 需要
--> 正在处理依赖关系 libcom_err(x86-64) = 1.42.9-12.el7_5，它被软件包 e2fsprogs-libs-1.42.9-12.el7_5.x86_64 需要
--> 正在处理依赖关系 libcom_err(x86-64) = 1.42.9-12.el7_5，它被软件包 e2fsprogs-1.42.9-12.el7_5.x86_64 需要
---> 软件包 libcom_err.x86_64.0.1.42.9-13.el7 将被 更新
---> 软件包 libselinux.i686.0.2.5-12.el7 将被 升级
---> 软件包 libselinux.x86_64.0.2.5-12.el7 将被 升级
--> 正在处理依赖关系 libselinux(x86-64) = 2.5-12.el7，它被软件包 libselinux-python-2.5-12.el7.x86_64 需要
--> 正在处理依赖关系 libselinux(x86-64) = 2.5-12.el7，它被软件包 libselinux-utils-2.5-12.el7.x86_64 需要
---> 软件包 libselinux.i686.0.2.5-14.1.el7 将被 更新
--> 正在处理依赖关系 libsepol(x86-32) >= 2.5-10，它被软件包 libselinux-2.5-14.1.el7.i686 需要
---> 软件包 libselinux.x86_64.0.2.5-14.1.el7 将被 更新
---> 软件包 libsepol-devel.x86_64.0.2.5-10.el7 将被 安装
---> 软件包 pcre-devel.x86_64.0.8.32-17.el7 将被 安装
--> 正在检查事务
---> 软件包 e2fsprogs.x86_64.0.1.42.9-12.el7_5 将被 升级
---> 软件包 e2fsprogs.x86_64.0.1.42.9-13.el7 将被 更新
---> 软件包 e2fsprogs-libs.x86_64.0.1.42.9-12.el7_5 将被 升级
---> 软件包 e2fsprogs-libs.x86_64.0.1.42.9-13.el7 将被 更新
---> 软件包 libselinux-python.x86_64.0.2.5-12.el7 将被 升级
---> 软件包 libselinux-python.x86_64.0.2.5-14.1.el7 将被 更新
---> 软件包 libselinux-utils.x86_64.0.2.5-12.el7 将被 升级
---> 软件包 libselinux-utils.x86_64.0.2.5-14.1.el7 将被 更新
---> 软件包 libsepol.i686.0.2.5-8.1.el7 将被 升级
---> 软件包 libsepol.x86_64.0.2.5-8.1.el7 将被 升级
---> 软件包 libsepol.i686.0.2.5-10.el7 将被 更新
---> 软件包 libsepol.x86_64.0.2.5-10.el7 将被 更新
---> 软件包 libss.x86_64.0.1.42.9-12.el7_5 将被 升级
---> 软件包 libss.x86_64.0.1.42.9-13.el7 将被 更新
--> 解决依赖关系完成

依赖关系解决

===========================================================================================================================================================================
 Package                                  架构                 版本                                   源                                                              大小
===========================================================================================================================================================================
正在安装:
 cloudera-manager-agent                   x86_64               6.3.0-1281944.el7                      /cloudera-manager-agent-6.3.0-1281944.el7.x86_64                61 M
为依赖而安装:
 MySQL-python                             x86_64               1.2.5-1.el7                            base                                                            90 k
 cups-client                              x86_64               1:1.6.3-35.el7                         base                                                           151 k
 cups-libs                                x86_64               1:1.6.3-35.el7                         base                                                           357 k
 cyrus-sasl-gssapi                        x86_64               2.1.26-23.el7                          base                                                            41 k
 fuse                                     x86_64               2.9.2-11.el7                           base                                                            86 k
 fuse-libs                                x86_64               2.9.2-11.el7                           base                                                            93 k
 httpd                                    x86_64               2.4.6-89.el7.centos.1                  updates                                                        2.7 M
 httpd-tools                              x86_64               2.4.6-89.el7.centos.1                  updates                                                         91 k
 keyutils-libs-devel                      x86_64               1.5.8-3.el7                            base                                                            37 k
 krb5-devel                               x86_64               1.15.1-37.el7_6                        updates                                                        271 k
 libcom_err-devel                         x86_64               1.42.9-13.el7                          base                                                            31 k
 libkadm5                                 x86_64               1.15.1-37.el7_6                        updates                                                        178 k
 libselinux-devel                         x86_64               2.5-14.1.el7                           base                                                           187 k
 libsepol-devel                           x86_64               2.5-10.el7                             base                                                            77 k
 libverto-devel                           x86_64               0.2.5-4.el7                            base                                                            12 k
 mailcap                                  noarch               2.1.41-2.el7                           base                                                            31 k
 mod_ssl                                  x86_64               1:2.4.6-89.el7.centos.1                updates                                                        112 k
 openssl-devel                            x86_64               1:1.0.2k-16.el7_6.1                    updates                                                        1.5 M
 pcre-devel                               x86_64               8.32-17.el7                            base                                                           480 k
 postgresql-libs                          x86_64               9.2.24-1.el7_5                         base                                                           234 k
 psmisc                                   x86_64               22.20-15.el7                           base                                                           141 k
 python-psycopg2                          x86_64               2.5.1-3.el7                            base                                                           132 k
 redhat-lsb-core                          x86_64               4.1-27.el7.centos.1                    base                                                            38 k
 redhat-lsb-submod-security               x86_64               4.1-27.el7.centos.1                    base                                                            15 k
 spax                                     x86_64               1.5.2-13.el7                           base                                                           260 k
 zlib-devel                               x86_64               1.2.7-18.el7                           base                                                            50 k
为依赖而更新:
 e2fsprogs                                x86_64               1.42.9-13.el7                          base                                                           699 k
 e2fsprogs-libs                           x86_64               1.42.9-13.el7                          base                                                           167 k
 krb5-libs                                x86_64               1.15.1-37.el7_6                        updates                                                        803 k
 libcom_err                               x86_64               1.42.9-13.el7                          base                                                            41 k
 libselinux                               i686                 2.5-14.1.el7                           base                                                           166 k
 libselinux                               x86_64               2.5-14.1.el7                           base                                                           162 k
 libselinux-python                        x86_64               2.5-14.1.el7                           base                                                           235 k
 libselinux-utils                         x86_64               2.5-14.1.el7                           base                                                           151 k
 libsepol                                 i686                 2.5-10.el7                             base                                                           294 k
 libsepol                                 x86_64               2.5-10.el7                             base                                                           297 k
 libss                                    x86_64               1.42.9-13.el7                          base                                                            46 k
 openssl                                  x86_64               1:1.0.2k-16.el7_6.1                    updates                                                        493 k
 openssl-libs                             x86_64               1:1.0.2k-16.el7_6.1                    updates                                                        1.2 M
 zlib                                     i686                 1.2.7-18.el7                           base                                                            91 k
 zlib                                     x86_64               1.2.7-18.el7                           base                                                            90 k

事务概要
===========================================================================================================================================================================
安装  1 软件包 (+26 依赖软件包)
升级           ( 15 依赖软件包)

总计：73 M
总下载量：12 M
Is this ok [y/d/N]: y
Downloading packages:
Delta RPMs disabled because /usr/bin/applydeltarpm not installed.
(1/41): MySQL-python-1.2.5-1.el7.x86_64.rpm                                                                                                         |  90 kB  00:00:05     
(2/41): cups-client-1.6.3-35.el7.x86_64.rpm                                                                                                         | 151 kB  00:00:05     
(3/41): cyrus-sasl-gssapi-2.1.26-23.el7.x86_64.rpm                                                                                                  |  41 kB  00:00:00     
(4/41): cups-libs-1.6.3-35.el7.x86_64.rpm                                                                                                           | 357 kB  00:00:00     
(5/41): e2fsprogs-libs-1.42.9-13.el7.x86_64.rpm                                                                                                     | 167 kB  00:00:00     
(6/41): fuse-2.9.2-11.el7.x86_64.rpm                                                                                                                |  86 kB  00:00:00     
(7/41): fuse-libs-2.9.2-11.el7.x86_64.rpm                                                                                                           |  93 kB  00:00:00     
(8/41): keyutils-libs-devel-1.5.8-3.el7.x86_64.rpm                                                                                                  |  37 kB  00:00:00     
(9/41): e2fsprogs-1.42.9-13.el7.x86_64.rpm                                                                                                          | 699 kB  00:00:00     
(10/41): httpd-tools-2.4.6-89.el7.centos.1.x86_64.rpm                                                                                               |  91 kB  00:00:04     
(11/41): krb5-devel-1.15.1-37.el7_6.x86_64.rpm                                                                                                      | 271 kB  00:00:00     
(12/41): libkadm5-1.15.1-37.el7_6.x86_64.rpm                                                                                                        | 178 kB  00:00:00     
(13/41): krb5-libs-1.15.1-37.el7_6.x86_64.rpm                                                                                                       | 803 kB  00:00:00     
(14/41): libselinux-2.5-14.1.el7.i686.rpm                                                                                                           | 166 kB  00:00:00     
(15/41): libselinux-devel-2.5-14.1.el7.x86_64.rpm                                                                                                   | 187 kB  00:00:00     
(16/41): libselinux-python-2.5-14.1.el7.x86_64.rpm                                                                                                  | 235 kB  00:00:00     
(17/41): libselinux-utils-2.5-14.1.el7.x86_64.rpm                                                                                                   | 151 kB  00:00:00     
(18/41): libsepol-2.5-10.el7.i686.rpm                                                                                                               | 294 kB  00:00:00     
(19/41): libsepol-2.5-10.el7.x86_64.rpm                                                                                                             | 297 kB  00:00:00     
(20/41): libsepol-devel-2.5-10.el7.x86_64.rpm                                                                                                       |  77 kB  00:00:00     
(21/41): libss-1.42.9-13.el7.x86_64.rpm                                                                                                             |  46 kB  00:00:00     
(22/41): libverto-devel-0.2.5-4.el7.x86_64.rpm                                                                                                      |  12 kB  00:00:00     
(23/41): mailcap-2.1.41-2.el7.noarch.rpm                                                                                                            |  31 kB  00:00:00     
(24/41): httpd-2.4.6-89.el7.centos.1.x86_64.rpm                                                                                                     | 2.7 MB  00:00:07     
(25/41): openssl-1.0.2k-16.el7_6.1.x86_64.rpm                                                                                                       | 493 kB  00:00:00     
(26/41): mod_ssl-2.4.6-89.el7.centos.1.x86_64.rpm                                                                                                   | 112 kB  00:00:01     
(27/41): openssl-libs-1.0.2k-16.el7_6.1.x86_64.rpm                                                                                                  | 1.2 MB  00:00:00     
(28/41): pcre-devel-8.32-17.el7.x86_64.rpm                                                                                                          | 480 kB  00:00:00     
(29/41): postgresql-libs-9.2.24-1.el7_5.x86_64.rpm                                                                                                  | 234 kB  00:00:00     
(30/41): psmisc-22.20-15.el7.x86_64.rpm                                                                                                             | 141 kB  00:00:00     
(31/41): python-psycopg2-2.5.1-3.el7.x86_64.rpm                                                                                                     | 132 kB  00:00:00     
(32/41): redhat-lsb-core-4.1-27.el7.centos.1.x86_64.rpm                                                                                             |  38 kB  00:00:00     
(33/41): redhat-lsb-submod-security-4.1-27.el7.centos.1.x86_64.rpm                                                                                  |  15 kB  00:00:00     
(34/41): spax-1.5.2-13.el7.x86_64.rpm                                                                                                               | 260 kB  00:00:00     
(35/41): zlib-1.2.7-18.el7.i686.rpm                                                                                                                 |  91 kB  00:00:00     
(36/41): zlib-1.2.7-18.el7.x86_64.rpm                                                                                                               |  90 kB  00:00:00     
(37/41): zlib-devel-1.2.7-18.el7.x86_64.rpm                                                                                                         |  50 kB  00:00:00     
(38/41): openssl-devel-1.0.2k-16.el7_6.1.x86_64.rpm                                                                                                 | 1.5 MB  00:00:01     
(39/41): libcom_err-1.42.9-13.el7.x86_64.rpm                                                                                                        |  41 kB  00:00:04     
(40/41): libcom_err-devel-1.42.9-13.el7.x86_64.rpm                                                                                                  |  31 kB  00:00:07     
(41/41): libselinux-2.5-14.1.el7.x86_64.rpm                                                                                                         | 162 kB  00:00:06     
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------
总计                                                                                                                                       649 kB/s |  12 MB  00:00:19     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  正在更新    : libcom_err-1.42.9-13.el7.x86_64                                                                                                                       1/57 
  正在更新    : zlib-1.2.7-18.el7.x86_64                                                                                                                              2/57 
  正在更新    : libsepol-2.5-10.el7.x86_64                                                                                                                            3/57 
  正在更新    : libselinux-2.5-14.1.el7.x86_64                                                                                                                        4/57 
  正在更新    : 1:openssl-libs-1.0.2k-16.el7_6.1.x86_64                                                                                                               5/57 
  正在更新    : krb5-libs-1.15.1-37.el7_6.x86_64                                                                                                                      6/57 
  正在更新    : 1:openssl-1.0.2k-16.el7_6.1.x86_64                                                                                                                    7/57 
  正在安装    : postgresql-libs-9.2.24-1.el7_5.x86_64                                                                                                                 8/57 
  正在安装    : psmisc-22.20-15.el7.x86_64                                                                                                                            9/57 
  正在安装    : python-psycopg2-2.5.1-3.el7.x86_64                                                                                                                   10/57 
  正在安装    : cyrus-sasl-gssapi-2.1.26-23.el7.x86_64                                                                                                               11/57 
  正在安装    : 1:cups-libs-1.6.3-35.el7.x86_64                                                                                                                      12/57 
  正在安装    : 1:cups-client-1.6.3-35.el7.x86_64                                                                                                                    13/57 
  正在安装    : libkadm5-1.15.1-37.el7_6.x86_64                                                                                                                      14/57 
  正在安装    : MySQL-python-1.2.5-1.el7.x86_64                                                                                                                      15/57 
  正在安装    : httpd-tools-2.4.6-89.el7.centos.1.x86_64                                                                                                             16/57 
  正在安装    : spax-1.5.2-13.el7.x86_64                                                                                                                             17/57 
  正在安装    : libsepol-devel-2.5-10.el7.x86_64                                                                                                                     18/57 
  正在安装    : zlib-devel-1.2.7-18.el7.x86_64                                                                                                                       19/57 
  正在安装    : libcom_err-devel-1.42.9-13.el7.x86_64                                                                                                                20/57 
  正在更新    : libss-1.42.9-13.el7.x86_64                                                                                                                           21/57 
  正在更新    : e2fsprogs-libs-1.42.9-13.el7.x86_64                                                                                                                  22/57 
  正在安装    : libverto-devel-0.2.5-4.el7.x86_64                                                                                                                    23/57 
  正在安装    : redhat-lsb-submod-security-4.1-27.el7.centos.1.x86_64                                                                                                24/57 
  正在安装    : redhat-lsb-core-4.1-27.el7.centos.1.x86_64                                                                                                           25/57 
  正在安装    : pcre-devel-8.32-17.el7.x86_64                                                                                                                        26/57 
  正在安装    : libselinux-devel-2.5-14.1.el7.x86_64                                                                                                                 27/57 
  正在安装    : mailcap-2.1.41-2.el7.noarch                                                                                                                          28/57 
  正在安装    : httpd-2.4.6-89.el7.centos.1.x86_64                                                                                                                   29/57 
  正在安装    : 1:mod_ssl-2.4.6-89.el7.centos.1.x86_64                                                                                                               30/57 
  正在安装    : fuse-2.9.2-11.el7.x86_64                                                                                                                             31/57 
  正在安装    : keyutils-libs-devel-1.5.8-3.el7.x86_64                                                                                                               32/57 
  正在安装    : krb5-devel-1.15.1-37.el7_6.x86_64                                                                                                                    33/57 
  正在安装    : 1:openssl-devel-1.0.2k-16.el7_6.1.x86_64                                                                                                             34/57 
  正在安装    : fuse-libs-2.9.2-11.el7.x86_64                                                                                                                        35/57 
  正在更新    : libsepol-2.5-10.el7.i686                                                                                                                             36/57 
  正在安装    : cloudera-manager-agent-6.3.0-1281944.el7.x86_64                                                                                                      37/57 
Created symlink from /etc/systemd/system/multi-user.target.wants/cloudera-scm-agent.service to /usr/lib/systemd/system/cloudera-scm-agent.service.
Created symlink from /etc/systemd/system/multi-user.target.wants/supervisord.service to /usr/lib/systemd/system/supervisord.service.
  正在更新    : e2fsprogs-1.42.9-13.el7.x86_64                                                                                                                       38/57 
  正在更新    : libselinux-python-2.5-14.1.el7.x86_64                                                                                                                39/57 
  正在更新    : libselinux-utils-2.5-14.1.el7.x86_64                                                                                                                 40/57 
  正在更新    : libselinux-2.5-14.1.el7.i686                                                                                                                         41/57 
  正在更新    : zlib-1.2.7-18.el7.i686                                                                                                                               42/57 
  清理        : libselinux-2.5-12.el7                                                                                                                                43/57 
  清理        : 1:openssl-1.0.2k-12.el7.x86_64                                                                                                                       44/57 
  清理        : e2fsprogs-1.42.9-12.el7_5.x86_64                                                                                                                     45/57 
  清理        : libsepol-2.5-8.1.el7                                                                                                                                 46/57 
  清理        : zlib-1.2.7-17.el7                                                                                                                                    47/57 
  清理        : 1:openssl-libs-1.0.2k-12.el7.x86_64                                                                                                                  48/57 
  清理        : krb5-libs-1.15.1-19.el7.x86_64                                                                                                                       49/57 
  清理        : libselinux-utils-2.5-12.el7.x86_64                                                                                                                   50/57 
  清理        : e2fsprogs-libs-1.42.9-12.el7_5.x86_64                                                                                                                51/57 
  清理        : libss-1.42.9-12.el7_5.x86_64                                                                                                                         52/57 
  清理        : libselinux-python-2.5-12.el7.x86_64                                                                                                                  53/57 
  清理        : libselinux-2.5-12.el7                                                                                                                                54/57 
  清理        : libsepol-2.5-8.1.el7                                                                                                                                 55/57 
  清理        : libcom_err-1.42.9-12.el7_5.x86_64                                                                                                                    56/57 
  清理        : zlib-1.2.7-17.el7                                                                                                                                    57/57 
  验证中      : fuse-libs-2.9.2-11.el7.x86_64                                                                                                                         1/57 
  验证中      : keyutils-libs-devel-1.5.8-3.el7.x86_64                                                                                                                2/57 
  验证中      : fuse-2.9.2-11.el7.x86_64                                                                                                                              3/57 
  验证中      : mailcap-2.1.41-2.el7.noarch                                                                                                                           4/57 
  验证中      : libsepol-2.5-10.el7.i686                                                                                                                              5/57 
  验证中      : MySQL-python-1.2.5-1.el7.x86_64                                                                                                                       6/57 
  验证中      : libcom_err-devel-1.42.9-13.el7.x86_64                                                                                                                 7/57 
  验证中      : pcre-devel-8.32-17.el7.x86_64                                                                                                                         8/57 
  验证中      : redhat-lsb-submod-security-4.1-27.el7.centos.1.x86_64                                                                                                 9/57 
  验证中      : krb5-devel-1.15.1-37.el7_6.x86_64                                                                                                                    10/57 
  验证中      : libselinux-2.5-14.1.el7.i686                                                                                                                         11/57 
  验证中      : httpd-2.4.6-89.el7.centos.1.x86_64                                                                                                                   12/57 
  验证中      : e2fsprogs-1.42.9-13.el7.x86_64                                                                                                                       13/57 
  验证中      : libverto-devel-0.2.5-4.el7.x86_64                                                                                                                    14/57 
  验证中      : zlib-devel-1.2.7-18.el7.x86_64                                                                                                                       15/57 
  验证中      : krb5-libs-1.15.1-37.el7_6.x86_64                                                                                                                     16/57 
  验证中      : zlib-1.2.7-18.el7.i686                                                                                                                               17/57 
  验证中      : python-psycopg2-2.5.1-3.el7.x86_64                                                                                                                   18/57 
  验证中      : zlib-1.2.7-18.el7.x86_64                                                                                                                             19/57 
  验证中      : 1:openssl-devel-1.0.2k-16.el7_6.1.x86_64                                                                                                             20/57 
  验证中      : psmisc-22.20-15.el7.x86_64                                                                                                                           21/57 
  验证中      : cyrus-sasl-gssapi-2.1.26-23.el7.x86_64                                                                                                               22/57 
  验证中      : cloudera-manager-agent-6.3.0-1281944.el7.x86_64                                                                                                      23/57 
  验证中      : 1:openssl-1.0.2k-16.el7_6.1.x86_64                                                                                                                   24/57 
  验证中      : httpd-tools-2.4.6-89.el7.centos.1.x86_64                                                                                                             25/57 
  验证中      : libss-1.42.9-13.el7.x86_64                                                                                                                           26/57 
  验证中      : libcom_err-1.42.9-13.el7.x86_64                                                                                                                      27/57 
  验证中      : libsepol-2.5-10.el7.x86_64                                                                                                                           28/57 
  验证中      : 1:openssl-libs-1.0.2k-16.el7_6.1.x86_64                                                                                                              29/57 
  验证中      : libsepol-devel-2.5-10.el7.x86_64                                                                                                                     30/57 
  验证中      : 1:cups-client-1.6.3-35.el7.x86_64                                                                                                                    31/57 
  验证中      : libselinux-python-2.5-14.1.el7.x86_64                                                                                                                32/57 
  验证中      : e2fsprogs-libs-1.42.9-13.el7.x86_64                                                                                                                  33/57 
  验证中      : 1:mod_ssl-2.4.6-89.el7.centos.1.x86_64                                                                                                               34/57 
  验证中      : 1:cups-libs-1.6.3-35.el7.x86_64                                                                                                                      35/57 
  验证中      : libselinux-utils-2.5-14.1.el7.x86_64                                                                                                                 36/57 
  验证中      : libkadm5-1.15.1-37.el7_6.x86_64                                                                                                                      37/57 
  验证中      : spax-1.5.2-13.el7.x86_64                                                                                                                             38/57 
  验证中      : libselinux-devel-2.5-14.1.el7.x86_64                                                                                                                 39/57 
  验证中      : redhat-lsb-core-4.1-27.el7.centos.1.x86_64                                                                                                           40/57 
  验证中      : postgresql-libs-9.2.24-1.el7_5.x86_64                                                                                                                41/57 
  验证中      : libselinux-2.5-14.1.el7.x86_64                                                                                                                       42/57 
  验证中      : e2fsprogs-1.42.9-12.el7_5.x86_64                                                                                                                     43/57 
  验证中      : libss-1.42.9-12.el7_5.x86_64                                                                                                                         44/57 
  验证中      : libsepol-2.5-8.1.el7.i686                                                                                                                            45/57 
  验证中      : 1:openssl-libs-1.0.2k-12.el7.x86_64                                                                                                                  46/57 
  验证中      : libselinux-python-2.5-12.el7.x86_64                                                                                                                  47/57 
  验证中      : zlib-1.2.7-17.el7.x86_64                                                                                                                             48/57 
  验证中      : zlib-1.2.7-17.el7.i686                                                                                                                               49/57 
  验证中      : e2fsprogs-libs-1.42.9-12.el7_5.x86_64                                                                                                                50/57 
  验证中      : libselinux-2.5-12.el7.i686                                                                                                                           51/57 
  验证中      : krb5-libs-1.15.1-19.el7.x86_64                                                                                                                       52/57 
  验证中      : libsepol-2.5-8.1.el7.x86_64                                                                                                                          53/57 
  验证中      : libcom_err-1.42.9-12.el7_5.x86_64                                                                                                                    54/57 
  验证中      : 1:openssl-1.0.2k-12.el7.x86_64                                                                                                                       55/57 
  验证中      : libselinux-2.5-12.el7.x86_64                                                                                                                         56/57 
  验证中      : libselinux-utils-2.5-12.el7.x86_64                                                                                                                   57/57 

已安装:
  cloudera-manager-agent.x86_64 0:6.3.0-1281944.el7                                                                                                                        

作为依赖被安装:
  MySQL-python.x86_64 0:1.2.5-1.el7                 cups-client.x86_64 1:1.6.3-35.el7                     cups-libs.x86_64 1:1.6.3-35.el7                                 
  cyrus-sasl-gssapi.x86_64 0:2.1.26-23.el7          fuse.x86_64 0:2.9.2-11.el7                            fuse-libs.x86_64 0:2.9.2-11.el7                                 
  httpd.x86_64 0:2.4.6-89.el7.centos.1              httpd-tools.x86_64 0:2.4.6-89.el7.centos.1            keyutils-libs-devel.x86_64 0:1.5.8-3.el7                        
  krb5-devel.x86_64 0:1.15.1-37.el7_6               libcom_err-devel.x86_64 0:1.42.9-13.el7               libkadm5.x86_64 0:1.15.1-37.el7_6                               
  libselinux-devel.x86_64 0:2.5-14.1.el7            libsepol-devel.x86_64 0:2.5-10.el7                    libverto-devel.x86_64 0:0.2.5-4.el7                             
  mailcap.noarch 0:2.1.41-2.el7                     mod_ssl.x86_64 1:2.4.6-89.el7.centos.1                openssl-devel.x86_64 1:1.0.2k-16.el7_6.1                        
  pcre-devel.x86_64 0:8.32-17.el7                   postgresql-libs.x86_64 0:9.2.24-1.el7_5               psmisc.x86_64 0:22.20-15.el7                                    
  python-psycopg2.x86_64 0:2.5.1-3.el7              redhat-lsb-core.x86_64 0:4.1-27.el7.centos.1          redhat-lsb-submod-security.x86_64 0:4.1-27.el7.centos.1         
  spax.x86_64 0:1.5.2-13.el7                        zlib-devel.x86_64 0:1.2.7-18.el7                     

作为依赖被升级:
  e2fsprogs.x86_64 0:1.42.9-13.el7           e2fsprogs-libs.x86_64 0:1.42.9-13.el7    krb5-libs.x86_64 0:1.15.1-37.el7_6         libcom_err.x86_64 0:1.42.9-13.el7        
  libselinux.i686 0:2.5-14.1.el7             libselinux.x86_64 0:2.5-14.1.el7         libselinux-python.x86_64 0:2.5-14.1.el7    libselinux-utils.x86_64 0:2.5-14.1.el7   
  libsepol.i686 0:2.5-10.el7                 libsepol.x86_64 0:2.5-10.el7             libss.x86_64 0:1.42.9-13.el7               openssl.x86_64 1:1.0.2k-16.el7_6.1       
  openssl-libs.x86_64 1:1.0.2k-16.el7_6.1    zlib.i686 0:1.2.7-18.el7                 zlib.x86_64 0:1.2.7-18.el7                

完毕！

```

创建cm数据库

```shell
[root@hadoop001 schema]# ./scm_prepare_database.sh mysql -h192.168.1.108 -uroot -p123456 --scm-host 192.168.1.109  scm2 root 123456
JAVA_HOME=/usr/java/jdk1.8.0_181-amd64
Verifying that we can write to /etc/cloudera-scm-server
Creating SCM configuration file in /etc/cloudera-scm-server
Executing:  /usr/java/jdk1.8.0_181-amd64/bin/java -cp /usr/share/java/mysql-connector-java.jar:/usr/share/java/oracle-connector-java.jar:/usr/share/java/postgresql-connector-java.jar:/opt/cloudera/cm/schema/../lib/* com.cloudera.enterprise.dbutil.DbCommandExecutor /etc/cloudera-scm-server/db.properties com.cloudera.cmf.db.
[                          main] DbCommandExecutor              INFO  Successfully connected to database.
All done, your SCM database is configured correctly!
```
修改cloudera agent 配置
```shell
[root@hadoop001 cloudera-scm-agent]# ls
config.ini
[root@hadoop001 cloudera-scm-agent]# vim config.ini

```

```shell
[root@hadoop001 cloudera-scm-agent]# systemctl start cloudera-scm-server
[root@hadoop001 cloudera-scm-agent]# systemctl status cloudera-scm-server
● cloudera-scm-server.service - Cloudera CM Server Service
   Loaded: loaded (/usr/lib/systemd/system/cloudera-scm-server.service; enabled; vendor preset: disabled)
   Active: active (running) since 四 2019-09-05 23:35:39 CST; 9s ago
 Main PID: 6131 (java)
   CGroup: /system.slice/cloudera-scm-server.service
           └─6131 /usr/java/jdk1.8.0_181-amd64/bin/java -cp .:/usr/share/java/mysql-connector-java.jar:/usr/share/java/oracle-connector-java.jar:/usr/share/java/postgresql-connector-java.j...

9月 05 23:35:39 hadoop001 systemd[1]: Started Cloudera CM Server Service.
9月 05 23:35:39 hadoop001 systemd[1]: Starting Cloudera CM Server Service...
9月 05 23:35:39 hadoop001 cm-server[6131]: JAVA_HOME=/usr/java/jdk1.8.0_181-amd64
9月 05 23:35:39 hadoop001 cm-server[6131]: Java HotSpot(TM) 64-Bit Server VM warning: ignoring option MaxPermSize=256m; support was removed in 8.0
9月 05 23:35:46 hadoop001 cm-server[6131]: ERROR StatusLogger No log4j2 configuration file found. Using default configuration: logging only errors to the console. Set system p...ion logging.
Hint: Some lines were ellipsized, use -l to show in full.
[root@hadoop001 cloudera-scm-agent]# systemctl status cloudera-scm-agent
● cloudera-scm-agent.service - Cloudera Manager Agent Service
   Loaded: loaded (/usr/lib/systemd/system/cloudera-scm-agent.service; enabled; vendor preset: disabled)
   Active: active (running) since 四 2019-09-05 22:58:31 CST; 37min ago
 Main PID: 1089 (cmagent)
   CGroup: /system.slice/cloudera-scm-agent.service
           └─1089 /usr/bin/python2 /opt/cloudera/cm-agent/bin/cm agent

9月 05 22:58:48 hadoop001 cm[1089]: [05/Sep/2019 22:58:48 +0000] 1089 MainThread agent        INFO     Chmod'ing /var/run/cloudera-scm-agent/supervisor/include to 0751
9月 05 22:58:48 hadoop001 cm[1089]: [05/Sep/2019 22:58:48 +0000] 1089 MainThread agent        INFO     Created /var/run/cloudera-scm-agent/cgroups
9月 05 22:58:48 hadoop001 cm[1089]: [05/Sep/2019 22:58:48 +0000] 1089 MainThread agent        INFO     Chmod'ing /var/run/cloudera-scm-agent/cgroups to 0751
9月 05 22:58:48 hadoop001 cm[1089]: [05/Sep/2019 22:58:48 +0000] 1089 MainThread agent        INFO     Re-using pre-existing directory: /var/run/cloudera-scm-agent/process
9月 05 22:58:48 hadoop001 cm[1089]: [05/Sep/2019 22:58:48 +0000] 1089 MainThread tmpfs        INFO     Successfully mounted tmpfs at /var/run/cloudera-scm-agent/process
9月 05 22:58:48 hadoop001 cm[1089]: [05/Sep/2019 22:58:48 +0000] 1089 MainThread logging      INFO     Logging to /var/log/cloudera-scm-agent/cloudera-scm-agent.log
9月 05 22:58:58 hadoop001 cm[1089]: status_server: added process group
9月 05 22:58:58 hadoop001 cm[1089]: flood: added process group
9月 05 22:58:58 hadoop001 cm[1089]: /opt/cloudera/cm-agent/lib/python2.7/site-packages/psutil/_pslinux.py:477: RuntimeWarning: dirty, writeback, mapped, commit_limit memory s...were set to 0
9月 05 22:58:58 hadoop001 cm[1089]: warnings.warn(msg, RuntimeWarning)
Hint: Some lines were ellipsized, use -l to show in full.
[root@hadoop001 cloudera-scm-agent]# systemctl enable cloudera-scm-server
[root@hadoop001 cloudera-scm-agent]# systemctl enable cloudera-scm-agent
```


```sql
CREATE DATABASE hive DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
CREATE DATABASE hue DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
CREATE DATABASE amon DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
CREATE DATABASE rman DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
CREATE DATABASE metastore DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
CREATE DATABASE sentry DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
CREATE DATABASE nav DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
CREATE DATABASE navms DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
CREATE DATABASE oozie DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;


GRANT ALL ON hive.* TO 'root'@'%' IDENTIFIED BY '123456';
GRANT ALL ON hue.* TO 'root'@'%' IDENTIFIED BY '123456';
GRANT ALL ON oozie.* TO 'root'@'%' IDENTIFIED BY '123456';
GRANT ALL ON amon.* TO 'root'@'%' IDENTIFIED BY '123456';
GRANT ALL ON rman.* TO 'root'@'%' IDENTIFIED BY '123456';
GRANT ALL ON metastore.* TO 'root'@'%' IDENTIFIED BY '123456';
GRANT ALL ON nav.* TO 'root'@'%' IDENTIFIED BY '123456';
GRANT ALL ON navms.* TO 'root'@'%' IDENTIFIED BY '123456';
GRANT ALL ON sentry.* TO 'root'@'%' IDENTIFIED BY '123456';
```
配置数据库
https://www.cloudera.com/documentation/enterprise/6/6.3/topics/install_cm_mariadb.html#install_cm_mariadb

允许mysql（mariadb）被远程访问
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '123456'；
flush privileges;
