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


### Test

{% comment %} 
  Set the name you want to search for here. 
  It is case-sensitive, so we will use filters to make it robust.
{% endcomment %}
{% assign target_name = "Alice" | downcase %}
{% assign total_count = 0 %}

<h2>Searching for occurrences of: <strong>Alice</strong></h2>

<ul>
  {% for post in site.posts %}
    {% if post.comments %}
      {% assign post_count = 0 %}
      
      {% for comment in post.comments %}
        {% comment %} Convert comment body to lowercase for accurate matching {% endcomment %}
        {% assign comment_text = comment.message | downcase %}
        
        {% if comment_text contains target_name %}
          {% comment.message | split: target_name %}
          {% assign parts = comment_text | split: target_name %}
          {% assign occurrences = parts.size | minus: 1 %}
          {% assign post_count = post_count | plus: occurrences %}
        {% endif %}
      {% endfor %}

      {% if post_count > 0 %}
        <li>
          <a href="{{ post.url | relative_url }}">{{ post.title }}</a>: 
          Found {{ post_count }} time(s)
        </li>
        {% assign total_count = total_count | plus: post_count %}
      {% endif %}
    {% endif %}
  {% endfor %}
</ul>

<hr>
<h3>Total Occurrences Across Site: {{ total_count }}</h3>
