---
layout: default
title: Doctrine
---

## Generate entities based on the existing properties (sf3): ##

{% highlight bash %}
php bin/console doctrine:generate:entities AppBundle:%entity%
{% endhighlight %}

## Update database schema based on the existing entities (sf3): ##

{% highlight bash %}
php bin/console doctrine:schema:update --force
{% endhighlight %}
