---
layout: default
title: eZ Publish / eZ Platform (templates)
---

## Get content name: ##

{% highlight smarty %}
{% raw %}
{{ ez_content_name(content) }}
{% endraw %}
{% endhighlight %}

## Get raw field value in current language: ##

{% highlight smarty %}
{% raw %}
{{ ez_field_value(content, '%field_name%') }}
{% endraw %}
{% endhighlight %}

## Render field: ##

{% highlight smarty %}
{% raw %}
{{ ez_render_field(content, '%field_name%') }}
{% endraw %}
{% endhighlight %}

## Check if field is empty: ##

{% highlight smarty %}
{% raw %}
{{ ez_is_field_empty(content, '%field_name%') }}
{% endraw %}
{% endhighlight %}

## Display location: ##

{% highlight smarty %}
{% raw %}
{{ render(controller('ez_content:viewLocation', {'locationId': %locationId%, 'viewType': 'full'})) }}
{% endraw %}
{% endhighlight %}
