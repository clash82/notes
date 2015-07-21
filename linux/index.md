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

## Clear directory: ##

{% highlight bash %}
rm -rf %path%
{% endhighlight %}

## Find file: ##

{% highlight bash %}
find %path% -name "%filename%"
{% endhighlight %}
