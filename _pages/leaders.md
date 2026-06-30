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

---
layout: page
title: "Comment Content Counter"
---

{% assign total_words = 0 %}
{% assign comment_count = 0 %}

{%- comment -%} Loop through both posts and pages {%- endcomment -%}
{% assign all_content = site.posts | concat: site.pages %}

{% for item in all_content %}
  {% if item.content contains '<!--' %}
    {%- comment -%} Split the content by the opening comment tag {%- endcomment -%}
    {% assign parts = item.content | split: '<!--' %}
    
    {% for part in parts %}
      {%- comment -%} Skip the first part because it is before the first comment {%- endcomment -%}
      {% if forloop.first %}{% continue %}{% endif %}
      
      {%- comment -%} Isolate the text inside the comment {%- endcomment -%}
      {% assign comment_pieces = part | split: '-->' %}
      {% assign comment_text = comment_pieces[0] | strip %}
      
      {%- comment -%} Count words and increment totals {%- endcomment -%}
      {% assign words = comment_text | number_of_words %}
      {% assign total_words = total_words | plus: words %}
      {% assign comment_count = comment_count | plus: 1 %}
    {% endfor %}
  {% endif %}
{% endfor %}

<h2>Site-Wide Comment Statistics</h2>
<ul>
  <li><strong>Total Comments Found:</strong> {{ comment_count }}</li>
  <li><strong>Total Words Inside Comments:</strong> {{ total_words }}</li>
</ul>
