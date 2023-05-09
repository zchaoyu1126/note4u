---
title: 日复一日，必有精进
sticky: 10
abbrlink: d12117ad
date: 2023-02-01 21:26:08
tags:
cover: http://img.note4u.top/base/dailylog_cover.jpg
---

## 2023.05.08


## 2023.05.04-2023.05.07
- 完成GSS文档
  - 文件加载、偏移校正、贴图旋转
  - 路径优化、结果输出
  - 绘图窗口、图形界面

## 2023.04.22-2023.04.27
- 整理GSS文档
  - 程序的运行
  - 加密狗与安装包制作
  - 背景知识
  - 区域分割、图形分割、反投影

## 2023.04.21
- 开始着手学习client-go

## 2023.04.20
- SSDFID 图像(20*5*5，500张) 
- 《K8S in Action》第四章笔记整理

## 2023.04.19
- 《K8S in Action》第三章笔记梳理

## 2023.04.18
- 完成[使用Docker构建镜像](http://note4u.top/post/78184262.html)


## 2023.02.13
- latex：三线表https://blog.csdn.net/weixin_44044161/article/details/116739166
- https://blog.csdn.net/TH_guan/article/details/124878398
- https://blog.csdn.net/DENGSHUCHAO152/article/details/122352913
- https://blog.csdn.net/UCB001/article/details/112546694


## 2023.02.12
- 发现问题！
  - 图像显示错误：https://blog.csdn.net/xsz591541060/article/details/108062438
- 柱状图：https://blog.csdn.net/iii66yy/article/details/124495337

## 2023.02.11
- 绘图与摸鱼中，懊悔！
- 绘图：
  - https://zhuanlan.zhihu.com/p/65116358
  - https://blog.csdn.net/weixin_43186872/article/details/122961584
- matlab:
  - 去除为0的元素：https://blog.csdn.net/SailingLT/article/details/80673556
  - saveas保存图片：https://blog.csdn.net/gls_nuaa/article/details/127251814
  - 小于阈值置零：https://blog.csdn.net/victor8370/article/details/120728028

## 2023.02.10
- 完成第三章大纲

## 2023.02.09
- 新增全局特征因子https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8168377&tag=1
- https://github.com/Atmegal/Sharpness-evaluation/blob/master/final.m
- 第一二章基本完成，但需要大修，降重

## 2023.02.08
- 更新[虚拟机与容器、Docker与K8S常见混淆点梳理](http://note4u.top/post/757d0b1c.html)

## 2023.02.07
- 调整权重函数，求加权平均
- 更新[云计算与云原生基本概念](http://note4u.top/post/6328194b.html)

## 2023.02.06
- matlab
  - 导入txt数据后是table类型，可使用table2cell
  - "hello world"是string类型，不可使用str(1:10)，需要将其转为char数组，即char(str)
  - 高斯模糊会导致边缘向外扩散

## 2023.02.05 


- 元宵：毫无长进的一天

## 2023.02.04
- 使用sigmod函数，将mlv值映射到-10到10之间，从而生成权重矩阵。
- reshape是按列读取的，在将经过mat2vec之后，还可以逆变换vec2mat
    ``` matlab
    clear;
    clc;

    %% read img and caculate map
    img = im2gray(imread("blur_4.png")); 
    map = mlvmap(img);

    % figure;
    % imshow(map, []);

    %% mat2vec
    % 将 map 变成一个向量
    [xs, ys] = size(map);
    total_number = xs * ys;
    vec = reshape(map, 1, total_number);
    vec = abs(vec);

    %% caculate weight
    [x, ~] = mapminmax(vec, -10, 10);
    alpha = 2;
    beta = 5;
    % f = @(x) 1.0 / (1+exp(-alpha*(x-beta)));
    weight = 1.0 ./ (1 +exp(-alpha * (x-beta)));

    %% select and caculate score
    svec = vec .* weight;
    selected = svec>=max(svec)*0.5;
    cnt = sum(selected(:));
    total_sum = sum(svec(selected==1));
    score = total_sum / cnt;
    fprintf("score:%f, totalSum:%f, cnt:%f\n", score, total_sum, cnt);
    ```
- 还需完成的工作：
  - 需要做一个图演示，演示权重函数
  - 怎么自适应得选择合适的像素点？
    
## 2023.02.03
- 主页隐藏部分文章
    - 更换首页生成插件，方法来自[链接](https://github.blog.ccknbc.cc/posts/how-to-hide-hexo-articles-gracefully/)
    ``` npm
    npm uninstall hexo-generator-index
    npm install hexo-generator-indexed
    ```
    - 修改butterfly主题(不推荐，存在一定问题)，方法来自[链接](https://blog.zhheo.com/p/451ff5e9.html)
- 完成[使用windows客户端连接阿里云ftp服务器](http://note4u.top/post/5a8a6c8d.html)
        
- 实验    
    - 2023_kadid10k_blur_result.mat
    - 2023_bid_result.mat
- 基于视觉感知的无参考模糊图像质量评价算法研究_雷初聪
- 根据mlvmap的分布，考虑设计一个权重函数，让变化值大的获得较大的权重，而变化值小的则快速衰减。
    
## 2023.02.02
- 查询进程pid：ps -ef | grep nginx
- 更新[使用windows客户端连接阿里云ftp服务器](http://note4u.top/post/5a8a6c8d.html)
    - 弃用windows资源管理器访问远程ftp服务器
    - 使用FileZilla访问ftp服务器
    - 阿里云轻量不支持FTP over TLS,只能使用明文


## 2023.02.01
- Telnet
    - 对于 windows powershell 测试端口是否开放时，可使用Telnet
    - 安装： 控制面板-->程序-->开启或关闭 windows 服务-->Telnet
    - 命令：telnet ip port
- yum
    - 安装：install，例，yum -y install vsftpd
    - 卸载：remove，例，yum remove vsftpd
- systemctl
    - 启动：start，例，systemctl start vsftpd
    - 停止：stop，例，systemctl stop vsftpd
    - 重启：restart，例，systemctl restart vsftpd
    - 是否开启：is-active，例，systemctl is-active vsftpd
- netstat
    - 查询ftp占用端口，netstat -antup | grep ftp
- [使用windows客户端连接阿里云ftp服务器](http://note4u.top/post/5a8a6c8d.html)
    - 200 Switching to ASCII mode 227 Entering Passive Mode
    - 200 Switching to ASCII mode 500 Illegal PORT command 500 Unkonwn command
    - 无法与服务器建立连接(未解决)

- 实验
    - 2023_tid2008_blur_result.mat
    - 2023_tid2013_blur_result.mat
    - 2023_csiq_blur_result.mat
    - 2023_live_blur_result.mat
    - 2023_kadid10k_blur01_result.mat
    - 2023_kadid10k_blur02_result.mat
    - 2023_kadid10k_blur03_result.mat