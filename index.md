---
title: /
layout: home
permalink: /
---

# Other Demo Pages

[Dark](https://b2a3e8.github.io/jekyll-theme-console-demo-dark/)  
[Hacker](https://b2a3e8.github.io/jekyll-theme-console-demo-hacker/)

# Welcome

Bla bla bla bla. Bla bla bla bla bla bla bla bla.

<div class="post-tags">
{% for tag in page.tags %}
  <a href="{{ '/tag/' | append: tag | relative_url }}" class="tag-link">#{{ tag }}</a>{% unless forloop.last %} {% endunless %}
{% endfor %}
</div>
