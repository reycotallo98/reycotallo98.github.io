---
layout: default
---
 
# Bienvenido a mi blog
## Aquí encontraras mis investigaciones y proyectos explicados a detalle, te invito a visitar las categorías:
<h2><a href="{{ site.baseurl }}/red">Red Team</a></h2>
<div class="posts">
  {% assign cont = 0 %}
  {% for post in site.posts %}
  {% if cont < 3 %}
  
 
   {% if post.category == "red" %}
  <article class="post">

      <h3><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h3>

      <div class="entry">
        {{ post.excerpt }}
      </div>

      <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">Seguir leyendo</a>
    </article>
  {% increment cont %}
   {% endif %}
   {% endif %}
  {% endfor %}
  {% if cont == 0 %}
  <p><strong>No se han encontrado artículos aún</strong></p>
   {% endif %}
  
</div>
<hr>
  <h2><a href="{{ site.baseurl }}/blue">Blue Team</a></h2>
<div class="posts">
  {% assign cont2 = 0 %}
  {% for post in site.posts %}
  {% if cont2 < 3 %}
 
 
   {% if post.category == "blue" %}
  <article class="post">

      <h3><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h3>

      <div class="entry">
        {{ post.excerpt }}
      </div>

      <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">Seguir leyendo</a>
    </article>
  {% increment cont2 %}
   {% endif %}
   {% endif %}
  {% endfor %}
  {% if cont2 == 0 %}
 <p><strong>No se han encontrado artículos aún</strong></p>
   {% endif %}
  </div>
 
  <hr>
  <h2><a href="{{ site.baseurl }}/dev">Desarrollo</a></h2>
<div class="posts">
  {% assign cont1 = 0 %}
  {% for post in site.posts %}
  {% if cont1 < 3 %}
 
 
   {% if post.category == "dev" %}
  <article class="post">

      <h3><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h3>

      <div class="entry">
        {{ post.excerpt }}
      </div>

      <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">Seguir leyendo</a>
    </article>
  {% increment cont1 %}
   {% endif %}
  {% endif %}
  {% endfor %}
  {% if cont1 == 0 %}
<p><strong>No se han encontrado artículos aún</strong></p>
   {% endif %}
</div>
