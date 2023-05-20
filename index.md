---
layout: default
---
 
# Bienvenido a mi blog
## Aquí encontraras mis investigaciones y proyectos explicados a detalle, te invito a visitar las categorías:
<h2><a href="{{ site.baseurl }}/red">Red Team</a></h2>
<div class="posts">
  {% assign cont = 0 %}
  {% for post in site.posts %}
  
  
 
   {% if post.category == "red" %}
  {% if cont < 3 %}
  <article class="post">

      <h2><a href="{{ site.baseurl }}{{ post.url }}" class="red">{{ post.title }}</a></h2>

      <div class="entry">
        {{ post.excerpt }}
      </div>

      <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">Seguir leyendo</a>
 <hr>
    </article>
  {% assign cont = cont | plus: 1 %}
   {% endif %}
   {% endif %}
  {% endfor %}
  {% if  cont == 0 %}
  <p><strong>No se han encontrado artículos aún</strong></p>
   {% endif %}
  
</div>

  <h2><a href="{{ site.baseurl }}/blue">Blue Team</a></h2>
<div class="posts">
  {% assign conta = 0 %}
  {% for post in site.posts %}
  
 
 
   {% if post.category == "blue" %}
  {% if conta < 3 %}
  <article class="post">

      <h2><a href="{{ site.baseurl }}{{ post.url }}" class="blue">{{ post.title }}</a></h2>

      <div class="entry">
        {{ post.excerpt }}
      </div>

      <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">Seguir leyendo</a>
 <hr>
    </article>
  {% assign conta = conta | plus: 1 %}
   {% endif %}
   {% endif %}
  {% endfor %}
  {% if conta == 0 %}
 <p><strong>No se han encontrado artículos aún</strong></p>
   {% endif %}
  </div>
 

  <h2><a href="{{ site.baseurl }}/dev">Desarrollo</a></h2>
<div class="posts">
  {% assign contb = 0 %}
  {% for post in site.posts %}
  {% if contb < 3 %}
 
 
   {% if post.category == "dev" %}
  <article class="post">

     <h2><a href="{{ site.baseurl }}{{ post.url }}" class="dev">{{ post.title }}</a></h2>

      <div class="entry">
        {{ post.excerpt }}
      </div>

      <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">Seguir leyendo</a>
 <hr>
    </article>
  {% assign contb = contb | plus: 1 %}
   {% endif %}
  {% endif %}
  {% endfor %}
 {% if contb == 0 %}
<p><strong>No se han encontrado artículos aún</strong></p>
   {% endif %}
</div>
