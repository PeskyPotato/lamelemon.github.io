---
layout: default
title: LameLemon
---

## /about

{:id="about"}

A software engineer that likes computer networking. My personal projects tend center around data preservation. 


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
