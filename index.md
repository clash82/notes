---
layout: default
title: ''
---

Choose your destiny:

<ul>
    {% for link in site.data.cheatsheet %}
        <li><a href="{{ link.link }}">{{ link.name }}</a></li>
    {% endfor %}
</ul>
