---
layout: default
title: ''
---

Plat du jour:

<ul>
    {% for link in site.data.cheatsheet %}
        <li><a href="{{ link.link }}">{{ link.name }}</a></li>
    {% endfor %}
</ul>

External links:

<ul>
    {% for link in site.data.links %}
        <li><a href="{{ link.url }}" target="_blank">{{ link.name }}</a></li>
    {% endfor %}
</ul>
