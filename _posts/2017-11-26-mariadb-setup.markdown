---
layout: post
title:  "Setup MariaDB (with password reset)"
date:   2017-11-26 22:22:22 +0200
tags:   nextcloud owncloud ubuntu mariadb
---
Seen this a tousand times and keeping to search for it every time. This is just a shortcut (and backup) for me.

root password reset:
{% highlight bash %}
service mysql stop
mysqld_safe --skip-grant-tables &
mysql -u root -D mysql

update user set password=PASSWORD("NEWPASSWORD") where User='root';
flush privileges;
exit;
{% endhighlight %}

create new database and user:
{% highlight bash %}
mysql -u root -p -D mysql

CREATE USER 'nextcloud'@'localhost' IDENTIFIED BY 'password';
CREATE DATABASE nextcloud;
GRANT ALL PRIVILEGES ON nextcloud . * TO 'nextcloud'@'localhost';
flush privileges;
exit;
{% endhighlight %}