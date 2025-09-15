---
layout: default
title: Brian Edwards' Technical Blog
---

<style>
  .page__content {
    padding: 2em; /* This adds padding to all four sides */
  }
</style>

<ul>
  {% for post in site.posts %}
    <li>
      <a href=".{{ post.url }}">{{ post.title }}</a>
      <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %d, %Y" }}</time>
    </li>
  {% endfor %}
</ul>
