---
layout: default
title: MySQL
---

## Dump database to file (format used in eZ Publish/Platform DemoBundle): ##

{% highlight bash %}
/usr/local/mysql/bin/mysqldump -u %username% --skip-add-drop-table --no-create-info --no-create-db --extended-insert=FALSE %database_name% > %filename.sql%
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

