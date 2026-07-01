---
title: Contributor Leader Board 
author: Graham Ambrose
date: 2026-06-29
category: Jekyll
layout: post 
---


<!-- Summary Counts of total Contributions -->

{% assign total_tags = 0 %}
{% for tag in site.tags %}
  {% assign tag_count = tag[1] | size %}
  {% assign total_tags = total_tags | plus: tag_count %}
{% endfor %}

<p><strong>{{ site.tags | size }} members </strong> of our community have contributed <strong>{{ total_tags  }}</strong> resources to produce this site.</p>



## Contributors by numbers of contributions:

<!-- Summary Counts at the Top -->

<div class="tag-cloud"> 
  {% for tag in site.tags %}
    {% assign name = tag | first %}
    {% assign count = tag | last | size %}
    <li>
    <!-- <a style="margin-right: 15px;">  href="#{{ name | slugify }}" -->
      {{ name }} ({{ count }})
    <!--</a>-->
    </li>
  {% endfor %}
</div>

<hr>

<h2>All Tags</h2>

{% comment %} 1. Create a padded string of 'count tag_name' separated by carets {% endcomment %}
{% capture tag_data %}
  {% for tag in site.tags %}
    {% assign tag_name = tag[0] | replace: ' ', '-' %}
    {% assign tag_count = tag[1].size | prepend: '0000' | slice: -4, 4 %}
    {{ tag_count }} {{ tag_name }}^{% endfor %}
{% endcapture %}

{% comment %} 2. Split into an array, sort alphabetically/numerically, and reverse for highest to lowest {% endcomment %}
{% assign sorted_tags = tag_data | split: '^' | sort | reverse %}

{% comment %} 3. Loop through the sorted array and render the tags {% endcomment %}
<ul>
  {% for item in sorted_tags %}
    {% unless item == empty %}
      {% assign parts = item | split: ' ' %}
      {% assign count = parts[0] | times: 1 %}
      {% assign name = parts[1] | replace: '-', ' ' %}

      <li>
        <a>
          {{ name }}
        </a>
        ({{ count }})
      </li>
    {% endunless %}
  {% endfor %}
</ul>


<!-- Detailed Section with Posts -->
<!--
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

<hr>
-->

<!-- Detailed Section with Posts -->
<!--
{% for tag in site.tags %}
  {% assign name = tag | first %}
  <h5 id="{{ name | slugify }}">{{ name }}</h5>
  <ul>
    {% for post in site.tags[name] %}
      {% assign name = post.title %}
      {% assign count = post.title | last | size %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ name }} ({{ count }})</a> 
      </li>
    {% endfor %}
  </ul>
{% endfor %}
-->

<!--
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

<div class="tag-cloud">
  <div class="extracted-content">
    {% assign gathered_content = "" | split: "" %}
  
    {% for post in site.posts %}
      {% assign extracted = post.content | split: '<div style="text-align: right"><i> submitted by ' %}
      {% for item in extracted %}
        {% if forloop.index0 > 0 %}
          {% assign content_piece = item | split: '</i></div>' | first %}
        
          {% assign count = item | last | size %}
          <a href="#{{ content_piece | slugify }}" style="margin-right: 15px;">
            {{ content_piece }} ({{ count }})
          </a>

        {% endif %}
      {% endfor %}
    {% endfor %}
  </div>
</div>

<hr>
-->
<!-- Detailed Section with Posts -->
<!-- 
<div class="extracted-content">
  {% assign gathered_content = "" | split: "" %}
  
  {% for post in site.posts %}
    {% assign extracted = post.content | split: '<div style="text-align: right"><i> submitted by ' %}
    {% for item in extracted %}
      {% if forloop.index0 > 0 %}
        {% assign content_piece = item | split: '</i></div>' | first | strip %}
        <h4 id="{{ content_piece | slugify }}">{{ content_piece }}</h4>
        <ul>
          {% for post in post.content[content_piece] %}
            <li>
              <a href="{{ post.url | relative_url }}">{{ post.title }}</a> 
            </li>
          {% endfor %}
        </ul>

      {% endif %}
    {% endfor %}
  {% endfor %}
</div>

### Test 3
-->