---
layout: default
title: 博客标签
permalink: /tags/
---

<div class="page-content wc-container">
    <h1>博客标签</h1><hr>
    <ul id="label_box">
        {% for tag in site.tags %}
            <li class="navigation-list"><a href="{{ site.baseurl }}/tags/#{{ tag[0] }}">{{ tag | first }}
            <span>({{ tag | last | size }})</span></a>
            </li>
        {% endfor %}
    </ul>
    <hr>
    {% for tag in site.tags %}
  <h3 id="{{ tag | first }}">{{ tag | first }}</h3>
  <!-- <span>{{ category | last | size }}</span> -->
  <ul class="arc-list">
      {% for post in tag.last %}
          <li>{{ post.date | date:"%d/%m/%Y"}} <a href="{{ post.url }}">{{ post.title }}</a></li>
      {% endfor %}
  </ul>
  {% endfor %}
</div>