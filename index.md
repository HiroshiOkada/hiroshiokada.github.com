---
layout: page
title: Hiroshi Okada's blog
tagline: 
---
{% include JB/setup %}

<ul class="posts">
  {% for post in site.posts %}
    {% unless post.unlist %}
    <li>
      <span>{{ post.date | date: "%Y-%m-%d" }}</span> 
      &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a> 
      : [<a href="/tags.html#{{ post.tags[0] }}-ref">{{ post.tags[0] }}]</a> 
    </li>
    {% endunless %}
  {% endfor %}
</ul>

