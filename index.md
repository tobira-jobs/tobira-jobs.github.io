---
layout: default
title: tobira jobs
---
## シゴトのトビラのヒミツの裏話
githubを活用していろんな話題を扱いたいと考えてます。
 - github pagesは基本的にmarkdownで書けるのでhtml記法を意識せずにサクサクかけて幸せ！  

最初はコンテンツも少ないし一度に完結した記事を上げられそうもないので  
同じページに内容を追加するような形で進めていきます。  
コンテンツの冒頭に目次を入れるようにし入門記事は投稿日昇順で  
時事ネタは最新が上に来るように登校日降順で管理したいと考えてます。

 - コメント欄を設けました。運用が安定するまではとりあえずこのページだけに置いておきます。  
   他のページのご意見もありましたらこのページのコメント欄にお書き下さい。

## 最近の投稿
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">最終更新日: {{ post.last_modified_at | default: post.date | date: "%Y-%m-%d" }} - {{ post.title }}
      </a>
    </li>
  {% endfor %}
</ul>

### コメント(ご自由にお書きください。)
<div id="cusdis_thread"
  data-host="https://cusdis.com"
  data-app-id="3729970e-7588-492c-a85a-0e1b780ebbb0"
  data-page-id="{{ 3729970e-7588-492c-a85a-0e1b780ebbb0 }}"
  data-page-url="{{ https://tobira-jobs.github.io/ }}"
  data-page-title="{{ HOME }}"
></div>
<script async defer src="https://cusdis.com/js/cusdis.es.js"></script>