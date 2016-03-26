---
layout: default
title: eZ Publish / eZ Platform (console)
---

## Install legacy assets: ##

{% highlight bash %}
php ezpublish/console ezpublish:legacy:assets_install --relative --symlink web
{% endhighlight %}

## Rebuild image aliases: ##

{% highlight bash %}
php ezpublish/console liip:imagine:cache:remove --filters=large
{% endhighlight %}
