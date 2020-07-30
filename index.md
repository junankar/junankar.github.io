---
title: Home
---

## Welcome to Software Development Knowledge Base 

This is my notebook of software development related stuff.

## Recent Posts
{% for post in site.posts limit:5 %}
<ul>
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
</ul>
{% endfor %}



