---
layout: default
title: Windows
---

Note: this is my private sheet which is dedicated to my common issues when working on Windows OS. Tips listed below are recommended only for power users.

## [10] Disable Windows Update service (update manually) to prevent killing my hard drive: ##

- open `Services` window and disable `Windows Update` service (alternatively open `Task manager`, go to the `Services` tab and search for `wuauserv` item and disable it permanently),
- reboot computer,
- completely remove `C:\Windows\SoftwareDistribution` folder,
- go to the `Event viewer` (type `eventvwr` in the Run command pane) and clear logs for `Application`, `Security`, `Setup` and `System log`.

## [10] Disable/enable Hyper-V without uninstalling it: ##

{% highlight bash %}
# disable
bcdedit /set {current} hypervisorlaunchtype off

# enable
bcdedit /set {current} hypervisorlaunchtype auto
{% endhighlight %}

Reboot machine after applying changes.

## [10] Disable Search Indexing service: ##

{% highlight bash %}
# disable
sc config "wsearch" start=disabled

# stop it right now
net stop "wsearch"
{% endhighlight %}

After that you can remove index file located at `C:\ProgramData\Microsoft\Search\Data\Applications\Windows\Windows.ebd`.


## [10] Disable SuperFetch service: ##

{% highlight bash %}
#disable
sc config "sysmain" start=disabled

# stop it right now
net stop "sysmain"
{% endhighlight %}

After that you can remove content of `C:\Windows\Prefetch` folder.
