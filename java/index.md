---
layout: default
title: Java
---

## [osx] Uninstall JDK completely: ##

{% highlight bash %}
sudo rm -rf /Library/Java/JavaVirtualMachines/jdk<version>.jdk

# run these commands if you want to remove plugins
sudo rm -rf /Library/PreferencePanes/JavaControlPanel.prefPane
sudo rm -rf /Library/Internet\ Plug-Ins/JavaAppletPlugin.plugin
sudo rm -rf /Library/LaunchAgents/com.oracle.java.Java-Updater.plist
sudo rm -rf /Library/PrivilegedHelperTools/com.oracle.java.JavaUpdateHelper
sudo rm -rf /Library/LaunchDaemons/com.oracle.java.Helper-Tool.plist
sudo rm -rf /Library/Preferences/com.oracle.java.Helper-Tool.plist
{% endhighlight %}
