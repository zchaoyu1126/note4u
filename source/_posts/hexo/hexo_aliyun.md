---
title: hexo部署到阿里云服务器
categories: hexo
abbrlink: 574ca0fa
date: 2022-10-13 22:23:28
tags: hexo
cover: http://img.note4u.top/base/hexo_cover.jpg
---

## 起因
起初，我使用Github Pages部署我的静态博客，并使用CNAME记录转发到`note4u.top`域名。过了一段时间后，阿里云提醒我，在阿里云购买的域名只能解析到阿里云的服务器，否则就要取消备案，所以我不得不将Hexo部署到阿里云轻量服务器上。

## 环境准备
- 笔记本(win10)
  - nodejs
  - git
  - hexo
- 阿里云轻量服务器(Centos 8.2)
  - git: yum -y install git
  - nginx: yum -y install nginx

## 生成SSH密钥
- 在笔记本上输入如下命令，在`C:\Users\UserName\.ssh`目录下生成密钥对
    ``` shell
    git config --global user.name "yourname"
    git config --global user.email "youremail"
    ssh-keygen -t rsa -C "youremail"
    ```

## 服务器配置
### 创建git账户并配置免密登录
- root: 登录服务器的root账户，创建git账户
    ``` shell
    adduser git
    ```
- root: 添加git账户权限
    ``` shell
    chmod 740 /etc/sudoers
    vim /etc/sudoers
    ```
    找到如下位置，添加`git  ALL=(ALL) ALL`，并保存
    ![20221014105346](http://img.note4u.top/article/20221014105346.png)
    ``` shell
    chmod 400 /etc/sudoers
    ```
- root: 设置git账户密码，并切换之git用户
    ``` shell
    sudo passwd git
    su git
    ```
- git: 创建` ~/.ssh/authorized_keys`文件
    ``` shell
    mkdir ~/.ssh
    vim ~/.ssh/authorized_keys
    ```
    将`C:\Users\UserName\.ssh\id_rsa.pub`文件中的公钥复制进去
    ![20221014110819](http://img.note4u.top/article/20221014110819.png)
    赋予权限
    ``` shell
    chmod 600 /home/git/.ssh/authorized_keys
    chmod 700 /home/git/.ssh
    ```
    在笔记本上使用`ssh -v git@SERVER`测试，若不需要密码登录则说明免密登录配置成功
### 创建git仓库目录与网站根目录
- root: 切换为root账户，并创建git仓库目录
    ``` shell
    sudo su root
    cd /home/git/
    git init --bare hexo.git
    chown -R git:git /home/git/hexo.git
    chmod -R 755 /home/git/hexo.git
    ```
- root: 创建网站根目录，并赋予权限
    ``` shell
    mkdir /home/git/site
    chown -R git:git /home/git/site
    chmod -R 755 /home/git/site
    ```
- root: 新增用于自动部署的Git钩子
    ``` shell
    cd /home/git/hexo.git
    vim hooks/post-receive
    ```
    将如下内容复制进去，注意`/home/git/site`和`/home/git/hexo.git`这两个路径信息
    ``` shell
    #!/bin/bash
    git --work-tree=/home/git/site --git-dir=/home/git/hexo.git checkout -f
    ```
    为新增的钩子赋予权限
    ``` shell
    chown -R git:git /home/git/hexo.git/hooks/post-receive
    chmod +x /home/git/hexo.git/hooks/post-receive
    ```
    通过进入`home/git/`目录中，输入`ll`命令检查权限是否正确
    ![20221016165648](http://img.note4u.top/article/20221016165648.png)

## 配置Nginx
- root: 修改nginx配置文件
    ``` shell
    vim  /etc/nginx/nginx.conf
    ```
    进行如下修改
    ![20230202195112](http://img.note4u.top/article/20230202195112.png)
- root: 检测nginx配置文件，重启nginx服务
    ``` shell
    /usr/sbin/nginx -t
    /usr/sbin/nginx -s reload
    ```

## 修改hexo配置
- 笔记本上编辑hexo的`_config.yml`文件
    ``` yaml
    deploy:
        type: git
        repository: git@xx.xx.xx.xx:/home/git/hexo.git
        branch: master
    ```
- 生成静态博客，并上传到服务器
    ``` shell
    hexo clean
    hexo g
    hexo d
    ```