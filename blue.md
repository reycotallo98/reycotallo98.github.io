---
layout: default
title: Blue team
permalink: /blue/
---
## Blue Team
### En este apartado se encuentran mis investigaciones y teoría en ciberdefensa.
 <hr>
<div class="posts">
  {% for post in site.posts %}
  {% if post.category == "blue" %}
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
