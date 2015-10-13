---
layout: default
title: eZ Publish / eZ Platform (known issues)
---

## You cannot create a service ("request") of an inactive scope ("request") ##

This issue occur when using legacy upon eZ Publish 5. Add this code to the `EzPublishKernel.php` file:

{% highlight php startinline %}
protected function initializeContainer() {
    parent::initializeContainer();
    if (PHP_SAPI == 'cli') {
        $this->getContainer()->enterScope('request');
        $this->getContainer()->set('request', new \Symfony\Component\HttpFoundation\Request(), 'request');
     }
}
{% endhighlight %}

## PHP Fatal error:  Cannot redeclare eZUpdateDebugSettings() (previously declared in ../ezpublish_legacy/kernel/classes/ezscript.php:1225) in .../ezpublish_legacy/kernel/private/classes/global_functions.php on line 109 ##

Add this line in `../vendor/ezsystems/legacy-bridge/mvc/kernel/Loader.php` file:

{% highlight php startinline %}
(...)

public function buildLegacyKernelHandlerCLI()
{
    $legacyRootDir = $this->legacyRootDir;
    $webrootDir = $this->webrootDir;
    $eventDispatcher = $this->eventDispatcher;
    $container = $this->container;
    $that = $this;

    return function () use ($legacyRootDir, $container, $eventDispatcher, $that) {
        if (!$that->getCLIHandler()) {
            $currentDir = getcwd();
            chdir($legacyRootDir);
     
            // add new line below   
            require_once 'kernel/private/classes/global_functions.php';
    
            $legacyParameters = new ParameterBag($container->getParameter('ezpublish_legacy.kernel_handler.cli.options'));

(...)
{% endhighlight %}

## The target directory "web" does not exist ##

This issue occur when using legacy upon eZ Publish 5 and trying to execute `assets:install` command. The simplest solution is to provide full path to `web` directory:

{% highlight bash startinline %}
php ezpublish/console asssets:install ~/Documents/%path%/web --symlink
{% endhighlight %}
