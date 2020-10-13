### Resetting user password via SQL command

```sql
UPDATE `ezuser` SET `password_hash_type`='5', `password_hash`='%plan_text_password%' WHERE `email`='%user_email%'
```

### Get content by contentId

```php
$contentService = $this->get('ezpublish.api.service.content');

$content = $contentService->loadContent($contentId);
```

### Get contentId by pathString

```php
$urlAliasService = $this->get('ezpublish.api.service.url_alias');
$locationService = $this->get('ezpublish.api.service.location');

$alias = $urlAliasService->lookup($pathString);
$contentId = $locationService->loadLocation($alias->destination)->contentId;
```

### Get content path string by content

```php
$urlAliasService = $this->get('ezpublish.api.service.url_alias');
$locationService = $this->get('ezpublish.api.service.location');

$pathString = $urlAliasService->reverseLookup(
    $locationService->loadLocation($content->contentInfo->mainLocationId)
)->path;
```

### Get content's UrlAlias based on contentId

```php
$contentService = $this->get('ezpublish.api.service.content');
$locationService = $this->get('ezpublish.api.service.location');
$urlService = $this->get('ezpublish.api.service.url_alias');

$content = $contentService->loadContent(68);
$location = $locationService->loadLocations($content->contentInfo);
$uri = $urlAlias->listLocationAliases($location['0'], false, 'eng-GB');
```

### Get ContentType identifier based on contentId

```php
$contentService = $this->get('ezpublish.api.service.content');
$contentTypeService = $this->get('ezpublish.get.service.content_type');

$contentTypeIdentifier = $contentTypeService->loadContentType(
    $contentService->loadContent($contentId)->contentInfo->contentTypeId
)->identifier;
```

### Get content data using sudo

```php
$repository = $this->get('ezpublish.api.repository');
$contentService = $this->get('ezpublish.api.service.content');

$result = $repository->sudo(
    function () use ($id, $contentService) {
        return $contentService->loadContentInfo($id);
    }
);
```

### Get content name (in template)

```twig
{% raw %}
{{ ez_content_name(content) }}
{% endraw %}
```

### Get raw field value in current language (in template)

```twig
{% raw %}
{{ ez_field_value(content, '%field_name%') }}
{% endraw %}
```

### Render field (in template)

```twig
{% raw %}
{{ ez_render_field(content, '%field_name%') }}
{% endraw %}
```

### Check if field is empty (in template)

```twig
{% raw %}
{{ ez_is_field_empty(content, '%field_name%') }}
{% endraw %}
```

### Display location (in template)

```twig
{% raw %}
{{ render(controller('ez_content:viewLocation', {'locationId': %locationId%, 'viewType': 'full'})) }}
{% endraw %}
```

### Display Twig version (in template)

```twig
{% raw %}
{{ constant('Twig_Environment::VERSION') }}
{% endraw %}
```

### Get siteaccess name (in template)

```twig
{% raw %}
{{ app.request.attributes.get('siteaccess').name }}
{% endraw %}
```
