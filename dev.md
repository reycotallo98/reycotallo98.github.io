---
layout: default
permalink: /dev/
title: Desarrollo
---
# Desarrollo
## En este apartado encontraréis artículos relacionados con el desarrollo, así como documentación o proyectos IOT.
<div class="posts">
  {% for post in site.posts.dev %}
  {% if post.category == "dev" %}
    <article class="post">

      <h2><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h2>

      <div class="entry">
        {{ post.excerpt }}
      </div>

      <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">Seguir leyendo</a>
    </article>
  <hr>
  {% endif  %}
  {% endfor %}
</div>
