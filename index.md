---
layout: page
title: Kernel Panic
tagline: 
---
{% include JB/setup %}

**Recent posts**:

{% for post in site.posts limit:1 %}
<span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
<span>{{post.content}}</span>
{% endfor %}

<ul class="posts">
    {% for post in site.posts offset:1 %}
    <li>
        <span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ul>
