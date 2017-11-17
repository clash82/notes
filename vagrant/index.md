---
layout: default
title: Vagrant
---

## Login to shell:  ##

{% highlight bash %}
vagrant ssh
{% endhighlight %}

## Start Vagrant: ##

{% highlight bash %}
vagrant up
{% endhighlight %}

## Stop Vagrant and clear data: ##

{% highlight bash %}
vagrant destroy
{% endhighlight %}

## Stop Vagrant but leave data: ##

{% highlight bash %}
vagrant halt
{% endhighlight %}

## Connect to MySQL in Vagrant with Sequel Pro: ##

{% highlight bash %}
SSH host: 127.0.0.1
SSH user: vagrant
SSH key: ~/.vagrant.d/insecureprivatekey
SSH port: 2222

default user/password: vagrant
{% endhighlight %}

## Disable time synchronisation: ##

{% highlight bash %}
# disable machine first (vagrant halt)
C:\Program Files\Oracle\VirtualBox\VBoxManage setextradata "%VM_NAME%" "VBoxInternal/Devices/VMMDev/0/Config/GetHostTimeDisabled" 1
# vagrant up
{% endhighlight %}
