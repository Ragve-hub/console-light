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
Контент содержит численные исследования финансового и экономического характера, проливающие свет на закономерности поведения биржевых цен в различных временных масштабах.
<br><br>


  {% assign date_format = "%Y-%m-%d" %}
  {% for tag in site.tags %}
  <div class="tags-item" id="{{ tag[0] }}">
    
    <h2 class="tags-item-label">{{ tag[0] }}</h2>
    {% for post in tag[1] %}
      <div>
        <time datetime="{{ post.date | date: date_format }}">[{{ post.date | date: date_format }}]</time>
        <a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
      </div>
    {% endfor %}
  </div>
  {% endfor %}
</div>
