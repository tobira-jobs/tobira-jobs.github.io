---
layout: default
title: Home
---
# シゴトのトビラの情報作成の裏話を書きますね
githubを活用していろんな話題を扱いたいと考えてます。

## 最近の投稿
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.date | date: "%Y-%m-%d" }} - {{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

