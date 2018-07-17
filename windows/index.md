---
layout: default
title: Windows
---

Note: this is my private sheet which is dedicated to my common issues when working on Windows OS. Tips listed below are recommended only for power users.

## [10] Disable Windows Update service (to prevent killing my hard drive): ##

- disable service from the elevated console:

{% highlight bash %}
# disable
sc config "wuauserv" start=disabled

# stop it right now
net stop "wuauserv"
{% endhighlight %}

Alternatively you can open `Services` window and disable `Windows Update` service (or open `Task manager`, go to the `Services` tab and search for `wuauserv` item and disable it permanently),

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
# disable
sc config "sysmain" start=disabled

# stop it right now
net stop "sysmain"
{% endhighlight %}

After that you can remove content of `C:\Windows\Prefetch` folder.

## [10] List devices that can wake computer up: ##

{% highlight bash %}
powercfg -devicequery wake_armed
{% endhighlight %}

From here, find the devices in your Device Manager (Control Panel) and, under the "Power Management" tab, remove their ability to wake your computer up. If you have network interface cards that you want to keep Wake-on-LAN for, enable "Only wake this device if it receives a magic packet" as opposed to waking up for all traffic sent its way.

## [ConEmu] Add `Git Bash here` to `ConEmu` in elevated mode: ##

- in ConEmu press `Win+Alt+p` to open the settings tab,
- select the `Tasks` subsection under the `Startup` node and click the `+` icon to add a new `Task`,
- in the `Task Name` field enter `Git Bash`, leave `Task Parameters` blank and add `"C:\Program Files\Git\bin\sh.exe" --login -i -new_console:a` to the `Commands` section,
- select the `Integration` node and enter the following under the `ConEmu Here - Explorer context menu integration` section:
* __Menu item__: `ConEmu Here [Git Bash]`
* __Command__: `/single /cmd {Git Bash}`
* __Icon file__: `C:\Program Files\Git\mingw64\share\git\git-for-windows.ico`
- click the `Register` button.
