---
layout: default
---
{:id="posts"}
<ul>
{% for post in site.categories.posts %}
    {% if post.parentPost == true %}
        <li><a href="{{ post.link }}">{{ post.title }}</a> - {{ post.description }}</li>
    {% endif %}
{% endfor %}
</ul>
