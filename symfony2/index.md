---
layout: default
title: Symfony 2
---

## Clear cache in production environment: ##

{% highlight bash %}
php app/console cache:clear -e=prod
{% endhighlight %}

## Dump assets: ##

{% highlight bash %}
php app/console assetic:dump
{% endhighlight %}

## Start assets watching: ##

{% highlight bash %}
php app/console assetic:watch
{% endhighlight %}

## Run built-in PHP server: ##

{% highlight bash %}
php app/console server:run
{% endhighlight %}

## Dump semantic configuration for specified reference: ##

{% highlight bash %}
php app/console config:dump-reference %reference_name%
{% endhighlight %}
