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
<section class="post-search" aria-label="搜索文章">
  <label class="search-label" for="post-search-input">检索文章</label>
  <input id="post-search-input" class="search-input" type="search" placeholder="搜索标题、正文或标签" autocomplete="off">
  <p id="post-search-count" class="search-count" aria-live="polite"></p>
</section>
<section id="post-list" class="post-list" aria-label="文章列表">
  {% for post in site.posts %}
  <article
    class="post-item"
    data-title="{{ post.title | strip_html | escape }}"
    data-content="{{ post.content | strip_html | strip_newlines | escape }}"
    data-tags="{{ post.tags | join: ' ' | escape }}"
    data-date="{{ post.date | date: '%Y-%m-%d' | escape }}"
  >
    <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%Y.%m.%d" }}</time>
    <div>
      <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
      <p>{{ post.description | default: post.excerpt | strip_html | truncate: 120 }}</p>
    </div>
  </article>
  {% else %}
  <p class="empty-state">还没有文章。打开墨客，写下第一篇。</p>
  {% endfor %}
  <p id="post-search-empty" class="empty-state" hidden>没有找到匹配的文章。</p>
</section>
<script>
  (() => {
    const input = document.getElementById('post-search-input');
    const count = document.getElementById('post-search-count');
    const empty = document.getElementById('post-search-empty');
    const posts = Array.from(document.querySelectorAll('#post-list .post-item'));
    if (!input || !count || !empty) return;

    const normalize = (value) => value.trim().toLocaleLowerCase();
    const escapeRegExp = (value) => value.replace(/[.*+?^${}()|[\]\\]/g, '\\$&');
    const highlight = (element, query) => {
      const original = element.textContent || '';
      if (!query) {
        element.textContent = original;
        return;
      }
      const regex = new RegExp(escapeRegExp(query), 'giu');
      const fragment = document.createDocumentFragment();
      let lastIndex = 0;
      let match;
      while ((match = regex.exec(original)) !== null) {
        if (match.index > lastIndex) {
          fragment.appendChild(document.createTextNode(original.slice(lastIndex, match.index)));
        }
        const mark = document.createElement('mark');
        mark.textContent = match[0];
        fragment.appendChild(mark);
        lastIndex = match.index + match[0].length;
      }
      if (lastIndex < original.length) {
        fragment.appendChild(document.createTextNode(original.slice(lastIndex)));
      }
      element.replaceChildren(fragment);
    };

    const update = () => {
      const query = normalize(input.value);
      let visible = 0;
      posts.forEach((post) => {
        const haystack = [post.dataset.title, post.dataset.content, post.dataset.tags, post.dataset.date]
          .filter(Boolean)
          .join(' ')
          .toLocaleLowerCase();
        const matches = !query || haystack.includes(query);
        const title = post.querySelector('h2 a');
        const summary = post.querySelector('div > p');
        post.hidden = !matches;
        post.classList.toggle('is-match', Boolean(query) && matches);
        if (title) highlight(title, query);
        if (summary) highlight(summary, query);
        if (matches) visible += 1;
      });
      count.textContent = query ? `找到 ${visible} 篇文章` : `共 ${visible} 篇文章`;
      empty.hidden = posts.length === 0 || visible > 0;
    };

    input.addEventListener('input', update);
    update();
  })();
</script>
