---
layout: post
title:  "Get LAMP Working in 5 Minutes on Ubuntu"
date:   2016-02-03 22:00:00 +0100
comments: true
categories: tech
---

Ubuntu and LAMP are both awesome. Here are the quick and clean steps to set up LAMP on ubuntu (using 15.04 currently).

1. Install Apache
    
   To install Apache you must install the package `apache2`.

        $ sudo apt-get install apache2

   To check if Apache is working, simply head to [localhost](http://localhost/) in the browser and it should show something.

2. Install PHP

   You will need the package `php5` and also `libapache2-mod-php5` in order to let it work with Apache.

        $ sudo apt-get install php5 libapache2-mod-php5
        $ sudo service apache2 restart

   To check if PHP is working, write a simple script
    
        $ sudo echo "<?php phpinfo();" > /var/www/html/phpinfo.php

   to see your [PHP information](http://localhost/phpinfo.php). Don't forget to delete it afterwards.

3. Install MySQL

   Install the `mysql-server` package and its PHP support. Choose a secure password when prompted.

        $ sudo apt-get install mysql-server php5-mysql
    
   Run `mysql_secure_installation` to secure MySQL.
        
        $ mysql_secure_installation

4. Install [phpMyAdmin](https://www.phpmyadmin.net/downloads/) (Optional)

