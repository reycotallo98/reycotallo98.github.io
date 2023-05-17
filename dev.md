---
layout: default
permalink: /dev/
---
<div class="posts">
  {% for post in site.posts.dev %}
  {% if post.category == "dev" %}
    <article class="post">

      <h1><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h1>

      <div class="entry">
        {{ post.excerpt }}
      </div>

      <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">Seguir leyendo</a>
    </article>
  {% endif  %}
  {% endfor %}
</div>
