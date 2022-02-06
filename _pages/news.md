---
layout: page
title: news
permalink: /news/
description: academic updates
nav: true
---


<div class="news">
  <div class="table-responsive">
  {% for item in site.news reversed %}
    {% assign currentdate = item.date | date: "%Y" %}
    {% if currentdate != date %}
      {% unless forloop.first %}</table></div>{% endunless %}
      <h2 class="year">{{currentdate}}</h2>
      <table class="table table-sm table-borderless">
      {% assign date = currentdate %}
    {% endif %}
        <tr>
          <td scope="row"><strong>{{ item.date | date: "%Y-%m-%d" }}</strong></td>
          <td>
            {% if item.inline %}
              {{ item.content | remove: '<p>' | remove: '</p>' | emojify }}
            {% else %}
              <a class="news-title" href="{{ item.url | relative_url }}">{{ item.title }}</a>
            {% endif %}
          </td>
        </tr>
  {% endfor %}
