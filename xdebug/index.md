---
layout: default
title: xDebug
---

## Installation and integration with PhpStorm: ##

- download latest <a href="https://xdebug.org/files/" target="_blank">xDebug</a> version depeneding on the current PHP configuration,
- save downloaded library into `php\ext` directory,
- configure PHP by applying additional `php.ini` settings listed below:

{% highlight ini %}
[Xdebug]
zend_extension=php_xdebug.dll
xdebug.remote_enable=1
xdebug.remote_port=9000
xdebug.scream=0
xdebug.cli_color=1
xdebug.remote_handler=dbgp
xdebug.remote_host=127.0.0.1
xdebug.trace_output_dir=c:\temp
xdebug.idekey=PHPSTORM
{% endhighlight %}

- install `Xdebug helper` for Chrome/Opera web browser,
- in the settings window of the above extension set `IDE` to `PhpStorm` with the default value `PHPSTORM`,
- in the PhpStorm `Run -> Edit configurations` window add new configuration by clicking green plus button and selecting `PHP Remote Debug` option,
- choose existing server configuration or add new one with those values:

{% highlight bash %}
Host: %working_host%
Port: 80
Debugger: Xdebug
IDE key (session id): PHPSTORM
{% endhighlight %}

## Working with xDebug and PhpStorm: ##

- open PhpStorm and select `Run -> Start listening for PHP Debug Connections` menu item,
- open Chrome/Opera and select `Debug` under `Debugging` button,
- set new breakpoint in the PhpStorm code window and refresh page.
