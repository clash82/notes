---
layout: default
title: eZ Publish / eZ Platform (known issues)
---

## Resetting user password via SQL command ##

{% highlight mysql %}
UPDATE `ezuser` SET `password_hash_type`='5', `password_hash`='%plan_text_password%' WHERE `email`='%user_email%'
{% endhighlight %}
