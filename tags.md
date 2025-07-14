---
title: /Теги
permalink: /tags/
---

<div class="tags">
  <div class="tags-header">
    <h2 class="tags-header-title">{{ page.title }}</h2>
    <div class="tags-header-line"></div>
  </div>
  <div class="tags-clouds">
    {% for tag in site.tags %}
      <a href="#{{ tag[0] }}">{{ tag[0] }}</a>
    {% endfor %}
  </div>
  {% for tag in site.tags %}
  <div class="tags-item" id="{{ tag[0] }}">
    
    <path
      d="M20.59 13.41l-7.17 7.17a2 2 0 0 1-2.83 0L2 12V2h10l8.59 8.59a2 2 0 0 1 0 2.82z"
    ></path>
    <line x1="7" y1="7" x2="7.01" y2="7"></line>
    
    <h2 class="tags-item-label">{{ tag[0] }}</h2>
    {% for post in tag[1] %}
      <a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
      <br>
    {% endfor %}
  </div>
  {% endfor %}
</div>
