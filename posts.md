---
layout: default
---
{:id="posts"}
<ul>
{% for post in site.categories.posts %}
<li><a href="{{ post.link }}">{{ post.title }}</a> - {{ post.description }}</li>
{% endfor %}
</ul>
