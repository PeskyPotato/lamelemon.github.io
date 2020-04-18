---
layout: default
title: LameLemon
---

## /about

{:id="about"}
I am a Python developer who occasionally dabbles with PHP. My personal projects tend to centre around data preservation and web scraping.

## /projects
{:id="projects"}
<ul>
{% for project in site.categories.projects  limit:10 %}
<li><a href="{{ project.link }}">{{ project.title }}</a> - {{ project.description }}</li>
{% endfor %}
</ul>

## /posts
{:id="posts"}
<ul>
{% for post in site.categories.posts limit:10%}
<li><a href="{{ post.link }}">{{ post.title }}</a> - {{ post.description }}</li>
{% endfor %}
</ul>

## /contact
{:id="contact"}

<a href="https://github.com/LameLemon" class ="link">
GitHub
</a>
&nbsp;
<a href="https://twitter.com/helep0d" class="link">
Twitter
</a>
