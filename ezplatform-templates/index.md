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

## Get field value: ##

{% highlight smarty %}
{% raw %}
{{ ez_field_value(content, '%field_name%') }}
{% endraw %}
{% endhighlight %}
