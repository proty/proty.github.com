---
title: News
layout: default
---

[RSS-Feed](/rss.xml)

<ul class="postlist">
{% for post in site.posts %}
  <li><span>{{post.date | date: "%d.%m.%Y"}}</span> &raquo; <a href="{{post.url}}">{{post.title}}</a></li>
{% endfor %}
</ul>
