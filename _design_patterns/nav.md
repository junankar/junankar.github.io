---
title: C++
layout: default
---

### C++

<ul> 
  {% for collection in site.collections %}
    {% assign collectionname = collection.label %}
	{% if collectionname == page.collection %}
		{% for doc in site[collectionname] %}
			{% unless doc.url == page.url %}
				<li><a href="{{ doc.url }}">{{ doc.title }}</a></li>
			{% endunless %}
		{% endfor %}		  
    {% endif %}
  {% endfor %}
</ul>