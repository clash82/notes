---
layout: default
title: Hardware
---

## Disable built-in hard disk password with data destroy: ##

You can check current HDD state by executing command below:

{% highlight bash %}
sudo hdparm -I /dev/sdX
{% endhighlight %}

If state is `frozen` then there is no way to clear password other than erasing all data on that disk.

To unfreeze disk you first need to enable suspend mode:

{% highlight bash %}
sudo systemctl suspend
{% endhighlight %}

Then you have to create a new password (will be overwritten anyway):

{% highlight bash %}
sudo hdparm --security-set-pass NULL /dev/sdX
{% endhighlight %}
 
And finally we are running erase command on that disk:

{% highlight bash %}
sudo hdparm --security-erase NULL /dev/sdX
{% endhighlight %}

This operation may take up to several hours, progress is not reported. After that all data will be destroyed and master password will be removed.
