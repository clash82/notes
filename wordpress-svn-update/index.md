---
layout: default
title: WordPress (plugin update procedure over SVN)
---

## Update WordPress SVN repository standard procedure: ##

This guide includes steps required to update existing plugin in the official WordPress SVN repository.

- checkout the existing SVN repo:

{% highlight bash %}
svn co https://plugins.svn.wordpress.org/%plugin_name% %plugin_local_dir%
{% endhighlight %}

- copy updated files to the `trunks` directory
- add new files to the repo:

{% highlight bash %}
svn add --force trunk/*
{% endhighlight %}

- commit trunk:

{% highlight bash %}
svn ci -m "Adding updated files for the v0.1.0 release"
{% endhighlight %}

- tag a new plugin version:

{% highlight bash %}
svn cp trunk tags/0.1.0
{% endhighlight %}

- check in the changes:

{% highlight bash %}
svn ci -m "Tagging version 0.1.0"
{% endhighlight %}
