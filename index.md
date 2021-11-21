---
layout: default
title: LameLemon
---

## /about

{:id="about"}
I don't do a lot of software development and I don't do a lot of system or network administration, but I do do a lot of everything. I may or may not update my posts on here but I do keep a steady feed of interesting information, nuggets of knowledge if you will, on [TIL](https://til.helep0d.xyz/). 

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
