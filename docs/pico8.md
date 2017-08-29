---
title: PICO-8 et bases de la programmation
layout: pico8
---

<ul>
  {% for post in site.pico8 %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
