---
layout: default
title: Linux
---

## [tmux] attach to existing sessions: ##

{% highlight bash %}
tmux attach
{% endhighlight %}

## [tmux] keyboard shortcuts: ##

{% highlight bash %}
Ctrl+B + C = new session
Ctrl+B + N = next session
Ctrl+B + W = session list
Ctrl-B + 1..9 = switch to specified session
Ctrl-D = kill current session
Ctrl+B + Shift+5 = split screen
Ctrl+B + Left/Right = move between screens
{% endhighlight %}

## [python] run dummy SMTP server for development purpose: ##

{% highlight bash %}
sudo python -m smtpd -n -c DebuggingServer localhost:25
{% endhighlight %}

## [bash] clear directory: ##

{% highlight bash %}
rm -rf %path%
{% endhighlight %}

## [bash] find file: ##

{% highlight bash %}
find %path% -name "%filename%"
{% endhighlight %}

## [bash] get size of element on disk: ##

{% highlight bash %}
du -hs %path%
{% endhighlight %}

## [bash] find string in files: ##

{% highlight bash %}
grep -r %string% *
{% endhighlight %}

## [bash] generate SSH keys and copy to destination machine: ##

{% highlight bash %}
ssh-keygen -t rsa -b 2048
ssh-copy-id %login%@%host%
{% endhighlight %}

## [bash] create symbolic link: ##

{% highlight bash %}
ln -s %file_path% %link_path%
{% endhighlight %}

## [bash] compress file with password: ##

{% highlight bash %}
zip -e %file_path% %archive_name%
{% endhighlight %}

## [bash] show Linux version: ##

{% highlight bash %}
lsb_release -a
{% endhighlight %}

## [bash] keep showing only important entries from logs: ##

{% highlight bash %}
tail -f var/logs/* | grep -E 'ERROR|CRITICAL'
{% endhighlight %}
