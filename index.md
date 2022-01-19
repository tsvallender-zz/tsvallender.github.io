---
title: Home
---

<section id="contents">
<div class="posts">
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
</div>
<div class="posts">
  <h2>Tabletop</h2>
  <ul id="post-list">
    {% for post in site.dungeons %}
      <li class="post">
        <a href="{{ post.url }}"><h4>{{ post.title }}</h4></a>
        <div class="post-excerpt">{{ post.excerpt }}</div>
        <a href="{{ post.url }}" class="read-more">Read more</a>
        <div class="date">{{ post.date | date_to_long_string }}</div>
      </li>
    {% endfor %}
  </ul>
</div>
<div class="posts">
  <h2>Articles</h2>
  <ul id="post-list">
    {% for post in site.articles %}
      <li class="post">
        <a href="{{ post.url }}"><h4>{{ post.title }}</h4></a>
        <div class="post-excerpt">{{ post.excerpt }}</div>
        <a href="{{ post.url }}" class="read-more">Read more</a>
        <div class="date">{{ post.date | date_to_long_string }}</div>
      </li>
    {% endfor %}
  </ul>
</div>
</section>