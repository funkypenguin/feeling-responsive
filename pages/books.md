---
layout: page
show_meta: false
subheadline: "Published and Upcoming"
title: "Books"
description: "The following books are published or in-flight"
header:
   image_fullwidth: "header_books_large.jpg"
   thumb: "header_books_thumb.jpg"
   caption: Old Books
   caption_url: http://www.flickr.com/photos/9458417@N03/13190693773
permalink: "/books/"
---
The following lists published or upcoming books I'm working on:

<div>
    {% for post in site.categories.book %}
    <div class="row">
      <div class="small-12 columns b60">
      <p class="subheadline"><span class="subheader">{% if post.categories %}{{ post.categories | join: ' &middot; ' }}{% endif %}</span> – {% if post.subheadline %}{{ post.subheadline }}{% endif %}</p>
      <h2><a href="{{ site.url }}{{ post.url }}">{{ post.title }}</a></h2>
      <p>
        {% if post.image.thumb %}<a href="{{ site.url }}{{ post.url }}" title="{{ post.title escape_once }}"><img src="{{ site.url }}/images/{{ post.image.thumb }}" class="alignleft" width="150" height="150" alt="{{ page.title escape_once }}"></a>{% endif %}

        {% if post.meta_description %}{{ post.meta_description | strip_html | escape }}{% elsif post.teaser %}{{ post.teaser | strip_html | escape }}{% endif %}

        <a href="{{ site.url }}{{ post.url }}" title="{{ site.data.language.read }} {{ post.title escape_once }}"><strong>{{ site.data.language.read_more }}</strong></a>
      </p>
    </div><!-- /.small-12.columns -->
  </div><!-- /.row -->
    {% endfor %}
</div>
