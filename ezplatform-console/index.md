---
layout: default
title: eZ Publish / eZ Platform (console)
---

## Clear cache in production environment: ##

{% highlight bash %}
php ezpublihs/console cache:clear -e=prod
{% endhighlight %}

## Dump assets: ##

{% highlight bash %}
php ezpublish/console assetic:dump
{% endhighlight %}

## Start assets watching: ##

{% highlight bash %}
php ezpublish/console assetic:watch
{% endhighlight %}

## Run built-in PHP server: ##

{% highlight bash %}
php ezpublish/console server:run
{% endhighlight %}

## Update eZ Platform using Composer: ##

{% highlight bash %}
git checkout master
git pull
composer update
{% endhighlight %}

## Install legacy assets: ##

{% highlight bash %}
php ezpublish/console ezpublish:legacy:assets_install --relative --symlink web
{% endhighlight %}
