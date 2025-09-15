---
layout: default
title: Brian Edwards' Technical Blog
---

<h1>{{ page.title }}</h1>

<ul>
  {% for post in site.posts %}
    <li>
      <a href="./{{ post.url }}">{{ post.title }}</a>
      <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %d, %Y" }}</time>
    </li>
  {% endfor %}
</ul>
