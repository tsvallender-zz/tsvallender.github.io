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
        <a href="{{ post.url }}" class="read-more">Read more</a>
        <div class="date">{{ post.date | date_to_long_string }}</div>
      </li>
    {% endfor %}
  </ul>
</section>