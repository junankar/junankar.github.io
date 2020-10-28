---
title: Home
---

## Welcome to Software Development Bookmarks 

This is my collection of bookmarks with brief summary.

## Recent Posts
{% for post in site.posts limit:5 %}
<ul>
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
</ul>
{% endfor %}

