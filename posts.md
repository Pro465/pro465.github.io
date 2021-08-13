---
layout: default
title: all posts
---

<ul>
  {% for post in site.posts %}
    <li>
      <span>
          <b><a href="{{ post.url }}">{{ post.title }}</a></b>
          <i>{{ post.description }}</i>
      </span>
    </li>
  {% endfor %}
</ul>
