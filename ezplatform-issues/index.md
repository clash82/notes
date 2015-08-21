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
