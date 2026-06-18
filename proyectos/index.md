---
layout: page
title: Proyectos
---

<ul class="project-list">
{% for post in site.posts %}
  <li class="project-card">
    <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
    <p class="project-date">{{ post.date | date: "%-d de %B, %Y" }}</p>
    <p>{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
  </li>
{% else %}
  <p>Todavia no hay proyectos publicados. Pronto habrá algo.</p>
{% endfor %}
</ul>
