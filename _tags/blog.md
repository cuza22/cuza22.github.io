---
name: blog
title: blog
---
{% for tag in site.tags %}
* [tag.name](site.baseurl/tags/tag.name)
{% endfor %}