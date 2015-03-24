---
layout: page
show_meta: false
subheadline: Projects I've worked on
title: "Projects"
description: "Projects"
permalink: "/projects/"
---
Projects:
<ul>
    {% for post in site.categories.project %}
    <li><a href="{{ site.url }}{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
</ul>
