---
layout: default
title: Blue team
permalink: /blue/
---
<div class="posts">
  {% for post in _blues %}
    <article class="post">

      <h1><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h1>

      <div class="entry">
        {{ post.excerpt }}
      </div>

      <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">Seguir leyendo</a>
    </article>
  {% endfor %}
</div>
