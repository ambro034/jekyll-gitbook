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



#### Contributors by the number of resources they contributed:

<!-- Summary Counts at the Top -->

<div class="tag-cloud"> 
  <ol type="1">
    {% for tag in site.tags %}
      {% assign name = tag | first %}
      {% assign count = tag | last | size %}
    
      <li>
        <!-- <a style="margin-right: 15px;">  href="#{{ name | slugify }}" -->
        <strong>{{ name }}</strong> ({{ count }})
        <!--</a>-->
      </li>
      
    {% endfor %}
  </ol>
</div>

<hr>

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