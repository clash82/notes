---
layout: default
title: eZ Publish / eZ Platform (PHP)
---

## Get content by contentId: ##

{% highlight php startinline %}
$contentService = $this->get('ezpublish.api.service.content');
$content = $contentService->loadContent($contentId);
{% endhighlight %}

## Get contentId by pathString: ##

{% highlight php startinline %}
$urlAliasService = $this->get('ezpublish.api.service.url_alias');
$locationService = $this->get('ezpublish.api.service.location');
$alias = $urlAliasService->lookup($pathString);
$contentId = $locationService->loadLocation($alias->destination)->contentId;
{% endhighlight %}

## Get content path string by content: ##

{% highlight php startinline %}
$urlAliasService = $this->get('ezpublish.api.service.url_alias');
$locationService = $this->get('ezpublish.api.service.location');
$pathString = $urlAliasService->reverseLookup(
    $locationService->loadLocation($content->contentInfo->mainLocationId)
)->path;
{% endhighlight %}
