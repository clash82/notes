---
layout: default
title: eZ Publish / eZ Platform (console)
---

## Clear cache in production environment: ##

`php ezpublihs/console cache:clear -e=prod`

## Dump assets: ##

`php ezpublish/console assetic:dump`

## Start assets watching: ##

`php ezpublish/console assetic:watch`

## Run built-in PHP server: ##

`php ezpublish/console server:run`

## Update eZ Platform using Composer: ##

`git checkout master
git pull
composer update`
