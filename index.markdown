---
title: Home
---

<section id="posts">
  <h2>Posts</h2>
  <ul id="post-list">
    {% for post in site.posts %}
      <li class="post">
        <a href="{{ post.url }}"><h4>{{ post.title }}</h4></a>
        <div class="post-excerpt">{{ post.excerpt }}</div>
      </li>
    {% endfor %}
  </ul>
</section>