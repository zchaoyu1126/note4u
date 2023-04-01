---
title: 使用windows访问阿里云ftp服务器
abbrlink: 5a8a6c8d
date: 2023-02-02 21:37:56
tags: ftp
cover: http://img.note4u.top/base/ftp_cover.jpg
---

> 注：以下部分内容摘自 [阿里云官网文档](https://help.aliyun.com/document_detail/60152.html#section-2l7-f44-t70)


## 关于FTP
FTP(File Transfer Protocol)，文件传输协议，基于C/S架构，支持主动和被动两种模式
- 主动模式(PORT)：客户端向FTP服务器发送端口信息，由服务器主动连接该端口。
- 被动模式(PASV)：FTP服务器开启并发送端口信息给客户端，由客户端连接该端口，服务器被动接受连接。

FTP支持三种认证模式：
- 匿名用户：任何人无需密码验证就可直接登录FTP服务器。不安全，一般只传输不重要的公开文件。
- 本地用户：通过Linux系统本地用户验证登录权限，相较于匿名用户模式更安全。
- 虚拟用户：通过虚拟用户验证登录权限，虚拟用户只能访问Linux系统为其提供的FTP服务，而不能访问Linux系统的其它资源。

## 软硬件
- windows 10
- Centos 8.2(阿里云轻量应用服务器)
- Filezilla


## 配置过程
### 安装vsfptd
``` shell
# 下载
yum install -y vsftpd              
# 设置开机自启动
systemctl enable vsftpd.service
# 启动vsftpd服务
systemctl start vsftpd.service
```
### 新建本地模式的用户
``` shell
adduser chao
passwd chao
# 创建一个供ftp服务使用的文件目录
mkdir /var/ftp/chao
# 修改目录的拥有者
chown -R chao:chao /var/ftp/chao
```
### 修改vsfptd的配置文件

安装完毕后，原文件内容如下：
``` shell
# Example config file /etc/vsftpd/vsftpd.conf
#
# The default compiled in settings are fairly paranoid. This sample file
# loosens things up a bit, to make the ftp daemon more usable.
# Please see vsftpd.conf.5 for all compiled in defaults.
#
# READ THIS: This example file is NOT an exhaustive list of vsftpd options.
# Please read the vsftpd.conf.5 manual page to get a full idea of vsftpd's
# capabilities.
#
# Allow anonymous FTP? (Beware - allowed by default if you comment this out).
anonymous_enable=NO
#
# Uncomment this to allow local users to log in.
local_enable=YES
#
# Uncomment this to enable any form of FTP write command.
write_enable=YES
#
# Default umask for local users is 077. You may wish to change this to 022,
# if your users expect that (022 is used by most other ftpd's)
local_umask=022
#
# Uncomment this to allow the anonymous FTP user to upload files. This only
# has an effect if the above global write enable is activated. Also, you will
# obviously need to create a directory writable by the FTP user.
# When SELinux is enforcing check for SE bool allow_ftpd_anon_write, allow_ftpd_full_access
#anon_upload_enable=YES
#
# Uncomment this if you want the anonymous FTP user to be able to create
# new directories.
#anon_mkdir_write_enable=YES
#
# Activate directory messages - messages given to remote users when they
# go into a certain directory.
dirmessage_enable=YES
#
# Activate logging of uploads/downloads.
xferlog_enable=YES
#
# Make sure PORT transfer connections originate from port 20 (ftp-data).
connect_from_port_20=YES
#
# If you want, you can arrange for uploaded anonymous files to be owned by
# a different user. Note! Using "root" for uploaded files is not
# recommended!
#chown_uploads=YES
#chown_username=whoever
#
# You may override where the log file goes if you like. The default is shown
# below.
#xferlog_file=/var/log/xferlog
#
# If you want, you can have your log file in standard ftpd xferlog format.
# Note that the default log file location is /var/log/xferlog in this case.
xferlog_std_format=YES
#
# You may change the default value for timing out an idle session.
#idle_session_timeout=600
#
# You may change the default value for timing out a data connection.
#data_connection_timeout=120
#
# It is recommended that you define on your system a unique user which the
# ftp server can use as a totally isolated and unprivileged user.
#nopriv_user=ftpsecure
#
# Enable this and the server will recognise asynchronous ABOR requests. Not
# recommended for security (the code is non-trivial). Not enabling it,
# however, may confuse older FTP clients.
#async_abor_enable=YES
#
# By default the server will pretend to allow ASCII mode but in fact ignore
# the request. Turn on the below options to have the server actually do ASCII
# mangling on files when in ASCII mode. The vsftpd.conf(5) man page explains
# the behaviour when these options are disabled.
# Beware that on some FTP servers, ASCII support allows a denial of service
# attack (DoS) via the command "SIZE /big/file" in ASCII mode. vsftpd
# predicted this attack and has always been safe, reporting the size of the
# raw file.
# ASCII mangling is a horrible feature of the protocol.
#ascii_upload_enable=YES
#ascii_download_enable=YES
#
# You may fully customise the login banner string:
#ftpd_banner=Welcome to blah FTP service.
#
# You may specify a file of disallowed anonymous e-mail addresses. Apparently
# useful for combatting certain DoS attacks.
#deny_email_enable=YES
# (default follows)
#banned_email_file=/etc/vsftpd/banned_emails
#
#
# You may specify an explicit list of local users to chroot() to their home
# directory. If chroot_local_user is YES, then this list becomes a list of
# users to NOT chroot().
# (Warning! chroot'ing can be very dangerous. If using chroot, make sure that
# the user does not have write access to the top level directory within the
# chroot)
#chroot_local_user=YES
#chroot_list_enable=YES
# (default follows)
#chroot_list_file=/etc/vsftpd/chroot_list
#
# You may activate the "-R" option to the builtin ls. This is disabled by
# default to avoid remote users being able to cause excessive I/O on large
# sites. However, some broken FTP clients such as "ncftp" and "mirror" assume
# the presence of the "-R" option, so there is a strong case for enabling it.
#ls_recurse_enable=YES
#
# When "listen" directive is enabled, vsftpd runs in standalone mode and
# listens on IPv4 sockets. This directive cannot be used in conjunction
# with the listen_ipv6 directive.
listen=NO
#
# This directive enables listening on IPv6 sockets. By default, listening
# on the IPv6 "any" address (::) will accept connections from both IPv6
# and IPv4 clients. It is not necessary to listen on *both* IPv4 and IPv6
# sockets. If you want that (perhaps because you want to listen on specific
# addresses) then you must run two copies of vsftpd with two configuration
# files.
# Make sure, that one of the listen options is commented !!
listen_ipv6=YES

pam_service_name=vsftpd
userlist_enable=YES
```
修改vsftpd.conf时，建议先做备份
```
cp /etc/vsftpd/vsftpd.conf /etc/vsftpd/vsftpd.conf.back
```

对vsftpd.conf的修改内容如下所示
``` shell
listen=YES
#listen_ipv6=YES

#文件末尾添加
#设置登陆后的主目录
local_root=/var/ftp/chao

allow_writeable_chroot=YES
chroot_local_user=YES
chroot_list_enbale=YES
chroot_list_file=/etc/vsftpd/chroot_list

# 启用被动模式
pasv_enable=YES
pasv_address=<云服务器的公网地址>
pasv_min_port=50000
pasv_max_port=50010
```

### 添加例外用户名单
chroot_list 文件中的用户，将被允许访问 /var/ftp/chao 之外的其他目录。
由于上述设置的原因，即使不需要这个功能，也必须添加 /etc/vsftpd/chroot_list 这个文件。
``` shell
vim /etc/vsftpd/chroot_list
```

### 重启服务
``` shell
systemctl restart vsftpd.service
```

### 修改防火墙配置
在控制台界面，开放21与50000-50010端口。
在主动模式下，仅开放21端口即可。使用被动模式时，还需使用50000-50010端口。
![20230203153905](http://img.note4u.top/article/20230203153905.png)

## 踩坑记录

### 使用Windows资源管理器访问FTP服务
目前，使用Chrome内核的浏览器，已不支持ftp://ip:port的方式访问FTP服务器。故尝试使用Windows资源管理器。
~~- 问题1：错误码 200 Switching to ASCII mode 227 Entering Passive Mode~~
~~- 解决办法：关闭被动FTP，源自[链接](https://blog.csdn.net/m0_45176278/article/details/126852664)~~
~~- 问题2：错误码 200 Switching to ASCII mode 500 Illegal PORT command 500 Unkonwn command.~~
~~- 解决办法：按此链接进行配置[链接](https://blog.csdn.net/qq_40695642/article/details/105848131)~~

在后续配置的时候发现，windows资源管理器访问FTP服务，非常不稳定，即使完成了配置，但仍会显示**无法连接服务器**的错误，故决定弃用Windows资源管理。

### 使用Filezilla访问FTP服务
- 问题：报不支持FTP_OVER_TLS的错误
- 原因及解决：本次配置使用的虚拟云主机可能不支持FTP_OVER_TLS的上传，所以需要使用不安全的明文密码登录。