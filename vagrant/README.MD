Vagrant使用教程
==================

基础环境
--------------------

* VirtualBox 5.1.8
    * 下载地址 https://www.virtualbox.org/wiki/Download_Old_Builds_5_1
    
* Vagrant 1.8.6  
    * 下载地址：https://releases.hashicorp.com/vagrant/1.8.6/
    * 切记根据自己的操作系统下载，同时分32位和64位

* Windows 额外工作
    * 可能需要配置环境变量
    * 安装Xshell命令行工具
    
    
启动虚拟机
-------------------
* box下载
    * ﻿链接：http://pan.baidu.com/s/1i5BfL45 密码：himr
    * 下载之后请确保文件名为ubuntu1404.box
* 添加box
    * vagrant box add ubuntu1404 ubuntu1404.box
* 初始化box
    * vagrant init ubuntu1404
    * vagrant ssh

对虚拟机优化
-------------------
* 替换源
    * sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak #备份
    * sudo vim /etc/apt/sources.list #修改源
        * 将文件内容替换成[源文件内容](ubuntu/apt/sources.list)
    * sudo apt-get update #更新列表
    
* L(A|N)MP
    * Ngnix
        * sudo apt-get install nginx
        * nginx -v
        
            `nginx version: nginx/1.4.6 (Ubuntu)`
        * 测试Nginx
            * curl -I 'http://127.0.0.1'
                
                `HTTP/1.1 200 OK
                 Server: nginx/1.4.6 (Ubuntu)
                 Date: Sat, 07 Jan 2017 07:49:41 GMT
                 Content-Type: text/html
                 Content-Length: 612
                 Last-Modified: Tue, 04 Mar 2014 11:46:45 GMT
                 Connection: keep-alive
                 ETag: "5315bd25-264"
                 Accept-Ranges: bytes`
    * Apache
        * sudo apt-get install apache2
        * apache2 -v
            
            `Server version: Apache/2.4.7 (Ubuntu)
             Server built:   Jul 15 2016 15:34:04`
        * 测试访问，此时不能访问，因为80端口被nginx占用了,可以先把nginx停掉
            * curl -I 'http://127.0.0.1'
            
                `HTTP/1.1 200 OK
                 Date: Sat, 07 Jan 2017 08:15:26 GMT
                 Server: Apache/2.4.7 (Ubuntu)
                 Last-Modified: Sat, 07 Jan 2017 07:17:45 GMT
                 ETag: "2cf6-5457bee51dd0d"
                 Accept-Ranges: bytes
                 Content-Length: 11510
                 Vary: Accept-Encoding
                 Content-Type: text/html`
        * 更改端口，将端口设置为8888
            * 修改 ports.conf 文件
            * curl -I 'http://127.0.0.1:8888'
                
                `HTTP/1.1 200 OK
                 Date: Sat, 07 Jan 2017 08:24:15 GMT
                 Server: Apache/2.4.7 (Ubuntu)
                 Last-Modified: Sat, 07 Jan 2017 07:17:45 GMT
                 ETag: "2cf6-5457bee51dd0d"
                 Accept-Ranges: bytes
                 Content-Length: 11510
                 Vary: Accept-Encoding
                 Content-Type: text/html`
            
    * Mysql
        * sudo apt-get install mysql-server  #服务器端
            * 安装期间会提示输入为mysql设置root密码，我这边不操作，直接enter 不设置密码
        * sudo apt-get install mysql-client  #客户端
            * mysql -uroot -p #测试连接库，上面安装服务端没有设置密码，这里直接enter进入
    * php
        * 安装php
            * sudo apt-get install php5-cli 
                * php -v
                  
                  `PHP 5.5.9-1ubuntu4.20 (cli) (built: Oct  3 2016 13:00:37)
                  Copyright (c) 1997-2014 The PHP Group
                  Zend Engine v2.5.0, Copyright (c) 1998-2014 Zend Technologies
                      with Zend OPcache v7.0.3, Copyright (c) 1999-2014, by Zend Technologies`
        * PHP扩展
            * php5-mcrypt 
            * php5-mysql
            * php5-gd
        * 支持apache2的php模块
            * sudo apt-get install libapache2-mod-php5
        * 支持nginx fastcgi
            * sudo apt-get install php5-cgi php5-fpm

* 端口转发 为了验证nginx是否按照成功~~
    *  8888 端口转发到 80 
        * http://127.0.0.1:8888/
    *  8889 端口转发到 8888
        * http://127.0.0.1:8889/
            
Vagrant高级配置
------------------------
* 网络设置
    
    `config.vm.network "private_network", ip: "192.168.199.01"`

   
    
    