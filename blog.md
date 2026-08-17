---
layout: default
title: 博客
permalink: /blog/
---
<section class="page-intro">
  <p class="eyebrow">ALL WRITINGS</p>
  <h1>博客</h1>
  <p>按时间阅读全部文章。</p>
</section>
<section class="post-list" aria-label="文章列表">
  {% for post in site.posts %}
  <article class="post-item">
    <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%Y.%m.%d" }}</time>
    <div>
      <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
      <p>{{ post.description | default: post.excerpt | strip_html | truncate: 120 }}</p>
    </div>
  </article>
  {% else %}
  <p class="empty-state">还没有文章。打开墨客，写下第一篇。</p>
  {% endfor %}
</section>
