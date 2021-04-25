---
layout: splash
permalink: /
hidden: true
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/mm-home-page-feature.jpg
excerpt: >
  Collection of bookmarks for programming, software design etc.<br />  
    
---

#### Recent Posts
{% for post in site.posts limit:5 %}
<ul>
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
</ul>
{% endfor %}
