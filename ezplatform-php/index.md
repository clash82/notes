---
layout: default
title: eZ Publish / eZ Platform (PHP)
---

## Get content by contentId: ##

`$contentService = $this->get('ezpublish.api.service.content');
$content = $contentService->loadContent($contentId);`

## Get contentId by pathString: ##

`$urlAliasService = $this->get('ezpublish.api.service.url_alias');
$locationService = $this->get('ezpublish.api.service.location');
$alias = $urlAliasService->lookup($pathString);
$contentId = $locationService->loadLocation($alias->destination)->contentId;`

## Get content path string by content: ##

`$urlAliasService = $this->get('ezpublish.api.service.url_alias');
$locationService = $this->get('ezpublish.api.service.location');
$pathString = $urlAliasService->reverseLookup(
    $locationService->loadLocation($content->contentInfo->mainLocationId)
)->path;`
