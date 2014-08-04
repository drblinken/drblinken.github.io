---
layout: default
title: Dr. Blinken's Notes
---


## Dr. Blinken's Notebook
This is really mostly a personal notebook, conveniently backuped and served by github.

Once in a while, I also write something like a blog post:



{% for post in site.posts %}
 *   {{ post.date | date_to_string }} [{{ post.title }}]({{ post.url}})
{% endfor %}

