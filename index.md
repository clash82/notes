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

Useful links:

<ul>
    {% for link in site.data.links %}
        <li><a href="//{{ link.url }}" target="_blank">{{ link.name }}</a></li>
    {% endfor %}
</ul>
