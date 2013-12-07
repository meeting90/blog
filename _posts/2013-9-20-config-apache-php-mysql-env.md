---
layout: post
description: 在windows中配置Apache+php+mysql环境
keywords: 配置l环境
title: 在windows中配置Apache+php+mysql环境
categories: [apache]
tags: [configuration]
group: archive
icon: book
---

{% include meeting90/setup %}


### 资源


Apache2.2或者更高版本[下载地址](http://httpd.apache.org/download.cgi)

php5.3或者更高版本 [下载地址](http://php.net/downloads.php)

mysql 5.1或更高版本 [下载地址](http://dev.mysql.com/downloads/mysql/)



### 安装步骤：


#### 安装apache



下载到安装文件，双击安装，按照向导安装即可。

#### 安装php


将其解压到PHP_DIR 文件夹（eg:D:/php）

在环境变量Path中添加;D:/php;D/php/ext

修改环境变量需要重启计算机

#### 安装mysql


按照向导安装即可


<!-- more -->

#### 配置Apache2.2 http.conf 文件


加载PHP module

搜索LoadModule 在其下添加两行：


> LoadModule php5\_module "D:/php/php5apache2\_2.dll"

> PHpIniDir "D:/php"


![php_module]({{BASE_PATH}}/images/posts/php_module.png)

添加对php index 的支持

![php_index]({{BASE_PATH}}/images/posts/php_index.png)

搜索DirectoryIndex 在其后加入index.php

添加php 类型支持

搜索AddType 在其后加入两行：

> AddType application/x-httpd-php .php

> AddType application/x-httpd-php .html

![php_AddType]({{BASE_PATH}}/images/posts/php_addtype.png)

修改访问权限

![access](/images/posts/access.png)

在 <Directory ".../htdocs">后加入如下访问权限：

> Header set Access-Control-Allow-Origin "*"


此外需要将LoadModule headers\_module modules/mod\_headers.so前的#去掉

#### 配置php文件php.ini


将php.ini-product 重命名为php.ini,设置extension_dir 为ext，将其前的分号去掉

![php extension_dir ]({{BASE_PATH}}/images/posts/php_extension_dir.png)

设置mysql 的extension

![mysql extension]({{BASE_PATH}}/images/posts/mysql_extension.jpg)

#### 测试


通过ip地址访问index.html，表示apache工作中

![apache works]({{BASE_PATH}}/images/posts/apache_works.png)

书写test.php,将文件放在htdocs文件夹下,访问host/test.php  这里host=114.212.82.207


> mysql\_connect("localhost", "root", "33063306") or die(mysql\_error());

> echo "Connected to MySQL<br/>";


****访问结果如下，表示apache+php+mysql配置成功****

![finish]({{BASE_PATH}}/images/posts/finish.jpg)
