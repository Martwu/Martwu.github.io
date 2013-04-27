---
layout: page
title: 主页
tagline: 广博、简易 —— 学习之路
---
{% include JB/setup %}

#找博主点右上角

主页暂时就这个鸟样

没办法，搞了一天，好累。先hold住

##文章列表
<ul class="posts">
{% for post in site.posts %}
<li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
{% endfor %}
</ul>
