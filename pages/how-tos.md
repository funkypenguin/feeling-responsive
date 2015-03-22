---
layout: page
show_meta: false
subheadline: "How-To"
redirect_from: /how-to/
redirect_from: /how-tos/
redirect_from: /howto/
title: "How to..."
description: "As I figure out stuff, I like to post it here"
permalink: "/howtos/"
---
The links below explain how to..
<ul>
    {% for post in site.categories.how-to %}
    <li><a href="{{ site.url }}{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
</ul>
