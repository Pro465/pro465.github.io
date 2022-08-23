---
layout: default
---

# About

hi and welcome! this is my personal blogging site.

# All posts
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
