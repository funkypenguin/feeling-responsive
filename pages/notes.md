---
layout: page
show_meta: false
subheadline: "Notes"
title: "Notes"
description: "Brief notes"
permalink: "/notes/"
---
The links below explain how to..
<ul>
    {% for post in site.categories.note %}
    <li><a href="{{ site.url }}{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
</ul>
