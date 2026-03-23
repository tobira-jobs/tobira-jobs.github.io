---
layout: default
title: Home
---
# Jekyllへようこそ！
GitHub.dev（ブラウザ）だけで運用するスタイルに移行中です。

## 最近の投稿
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.date | date: "%Y-%m-%d" }} - {{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

