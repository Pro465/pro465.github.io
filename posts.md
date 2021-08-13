---
layout: default
title: all posts
description: A list of all posts with their desciptions
---

<ul>
  {% for post in site.posts %}
    <li>
      <span>
          <a href="{{ post.url }}">{{ post.title }}</a>:
          <i>{{ post.description }}</i>
      </span>
    </li>
  {% endfor %}
</ul>
