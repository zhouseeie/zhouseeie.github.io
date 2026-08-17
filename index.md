---
layout: default
title: 首页
---
<section class="home-intro">
  <p class="eyebrow">A QUIET PLACE FOR WRITING</p>
  <h1>写下值得留下的文字。</h1>
  <p>这里是 {{ site.title }}。记录想法、经验和正在慢慢形成的答案。</p>
  <p class="home-link"><a href="{{ '/blog/' | relative_url }}">进入博客 →</a></p>
</section>
<section class="home-latest" aria-labelledby="latest-title">
  <div class="section-heading">
    <h2 id="latest-title">最近文章</h2>
    <a href="{{ '/blog/' | relative_url }}">查看全部</a>
  </div>
  {% for post in site.posts limit: 3 %}
  <article class="post-item">
    <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%Y.%m.%d" }}</time>
    <div>
      <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
      <p>{{ post.description | default: post.excerpt | strip_html | truncate: 120 }}</p>
    </div>
  </article>
  {% else %}
  <p class="empty-state">还没有文章。打开墨客，写下第一篇。</p>
  {% endfor %}
</section>
