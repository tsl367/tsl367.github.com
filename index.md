---
layout: page
title: Just for Sharing and Enjoying!
tagline: A Programer's note
---
{% include JB/setup %}

## Recent Articles

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
