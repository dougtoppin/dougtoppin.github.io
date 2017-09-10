---
layout: post
title: "Tiny Tiny RSS"
date: 2014-02-15 22:18
comments: true
categories: 
---


[root@ip-10-28-253-41 ~]# sudo -u postgres psql
could not change directory to "/root"
psql (9.2.6)
Type "help" for help.

postgres=# CREATE USER "www-data" WITH PASSWORD 'julk57HH';
CREATE ROLE
postgres=# CREATE DATABASE ttrss WITH OWNER "www-data";
CREATE DATABASE
postgres=# \quit



sudo yum install php-mbstring
sudo yum install php-xml

sudo service httpd restart

sudo vim /var/lib/pgsql9/data/pg_hba.conf
insert 'local all all md5'

http://ec2-75-101-216-190.compute-1.amazonaws.com/tt-rss/install/


sudo chmod -R 777 cache/images/
sudo chmod -R 777 cache/upload
sudo chmod -R 777 cache/export
sudo chmod -R 777 cache/js
sudo chmod -R 777 feed-icons/
sudo chmod -R 777 lock


