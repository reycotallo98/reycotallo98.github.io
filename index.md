---
layout: default
---

# Bienvenido a mi blog
## Aquí encontraras mis investigaciones y proyectos explicados a detalle, te invito a visitar las categorías:
### Red Team
<div class="posts">
  {% assign cont = 0 %}
  {% for post in site.posts %}
   
  <article class="post">

      <h1><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h1>

      <div class="entry">
        {{ post.excerpt }}
      </div>

      <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">Seguir leyendo</a>
    </article>
  {% endfor %}
</div>
