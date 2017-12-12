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

## Move vendor directory to a different location: ##

This is very useful if you want to speed-up your work with Symfony in Vagrant VM (move `vendor` directory inside your Vagrant Box file structure).

- go to the sf2 project root directory
- remove `vendor` directory
- create `vendor` directory in new location (eg. `/home/vagrant/sf2_vendor`):

{% highlight bash %}
mkdir /home/vagrant/sf2_vendor
{% endhighlight %}

- symlink new directory:

{% highlight bash %}
ln -s /home/vagrant/sf2_vendor vendor
{% endhighlight %}

- run `composer install` again
- ignore `vendor` file globally in Git:

{% highlight bash %}
git config --global core.excludesfile '~/.gitignore_global'
vim ~/.gitignore_global
{% endhighlight %}

- optional: include new `vendor` path in PhpStorm (Settings &raquo; PHP &raquo; inlude path)