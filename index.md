---
layout: page
title: Kernel Panic
tagline: 
---
{% include JB/setup %}

<!--<img src="http://www.gravatar.com/avatar/0ce902c144b039ea818cea3cb7411981.png"/>-->

Recent posts:

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
