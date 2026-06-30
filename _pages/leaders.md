---
title: Contributor Leader Board 
author: Graham Ambrose
date: 2026-06-29
category: Jekyll
layout: post 
---

<!-- Summary Counts of total Contributions -->

{% assign target_string = "%&%" %}
{% assign total_count = 0 %}

{% comment %} Loop through all blog posts {% endcomment %}
{% for post in site.posts %}
  {% if post.content contains target_string %}
    {% assign parts = post.content | split: target_string %}
    {% assign occurrences = parts.size | minus: 1 %}
    {% assign total_count = total_count | plus: occurrences %}
  {% endif %}
{% endfor %}

<p>Our community has contributed <strong>{{ total_count }}</strong> resources to produce this site.</p>



## Tags by Count

<!-- Summary Counts at the Top -->
<div class="tag-cloud">
  {% for tag in site.tags %}
    {% assign name = tag | first %}
    {% assign count = tag | last | size %}
    <a href="#{{ name | slugify }}" style="margin-right: 15px;">
      {{ name }} ({{ count }})
    </a>
  {% endfor %}
</div>

<hr>

<!-- Detailed Section with Posts -->
{% for tag in site.tags %}
  {% assign name = tag | first %}
  <h4 id="{{ name | slugify }}">{{ name }}</h4>
  <ul>
    {% for post in site.tags[name] %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a> 
      </li>
    {% endfor %}
  </ul>
{% endfor %}

## Test

<div class="extracted-content">
  {% assign gathered_content = "" | split: "" %}
  
  {% for post in site.posts %}
    {% assign extracted = post.content | split: '<div style="text-align: right"><i> submitted by ' %}
    {% for item in extracted %}
      {% if forloop.index0 > 0 %}
        {% assign content_piece = item | split: '</i></div>' | first | strip %}
        {% assign gathered_content = gathered_content | push: content_piece %}
      {% endif %}
    {% endfor %}
  {% endfor %}

  {% for item in gathered_content %}
    <div class="right-aligned-item">
      {{ item }}
    </div>
  {% endfor %}
</div>

### Test 2

<div class="extracted-content">
  {% assign gathered_content = "" | split: "" %}
  
  {% for post in site.posts %}
    {% assign extracted = post.content | split: '<div style="text-align: right"><i> submitted by ' %}
    {% for item in extracted %}
      {% if forloop.index0 > 0 %}
        {% assign content_piece = item | split: '</i></div>' | first | strip %}
        
        {% assign name = content_piece | first %}
        {% assign count = content_piece | last | size %}
        <a href="#{{ name | slugify }}" style="margin-right: 15px;">
          {{ name }} ({{ count }})
        </a>

      {% endif %}
    {% endfor %}
  {% endfor %}
</div>

### Test 3


