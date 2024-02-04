---
layout: page
title: news
permalink: /news/
description: academic updates
nav: true
---


<div class="news">
  <div class="table-responsive">
  {% for y in (2020..2024) reversed %}
  <table class="table table-sm table-borderless">
  <h2 class="year">{{y}}</h2>
  {% for item in site.news reversed %}
    {% assign currentdate = item.date | date: "%Y" %}
    {% assign currentdate = currentdate | times: 1 %}
    {% if currentdate == y %}
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
    {% else %}
      {% continue %}
    {% endif %}
  {% endfor %}

  {% endfor %}
