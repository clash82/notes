---
layout: default
title: MySQL
---

## Dump database to file: ##

{% highlight bash %}
/usr/local/mysql-5.6.22-osx10.8-x86_64/bin/mysqldump -u %username% --skip-add-drop-table --no-create-info --no-create-db %database_name% > %filename.sql%
{% endhighlight %}

## Login to shell: ##

{% highlight bash %}
mysql -u %username% -p
{% endhighlight %}

## Change password for database: ##

{% highlight mysql %}
SET PASSWORD FOR '%username%'@'%hostname%' = PASSWORD('%new_password%');
{% endhighlight %}

## Import sql file from shell: ##

{% highlight mysql %}
use %database%
source %filename%;
{% endhighlight %}

## Reset auto-increment value: ##

{% highlight mysql %}
ALTER TABLE %table_name% AUTO_INCREMENT=%value%
{% endhighlight %}

