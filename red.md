---
layout: default
permalink: /red/
title: Red Team
---
#Red Team
## En esta sección encontraras herramientas, walkthroughts de máquinas así como investigaciones en el área del ciberataque.
<div class="posts">
  {% for post in site.posts.red %}
  {% if post.category == "red" %}
    <article class="post">

      <h2><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h2>

      <div class="entry">
        {{ post.excerpt }}
      </div>

      <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">Seguir leyendo</a>
    </article>
  <hr>
  {% endif %}
  {% endfor %}
</div>
