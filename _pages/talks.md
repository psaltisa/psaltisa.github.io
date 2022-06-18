---
layout: page
permalink: /talks/
title: presentations
description:
nav: true
---

<script type='text/javascript' src='https://d1bxh8uas1mnw7.cloudfront.net/assets/embed.js'></script>

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid" src="{{ site.baseurl }}/assets/img/about3.JPG" alt="" title=""/>
    </div>
</div>
<div class="caption">
    Presenting at the 23rd Symposium of the Hellenic Nuclear Physics Society in Thessaloniki, Greece (2014).
</div>


<div class="news">  
   <h2>talks</h2>
  <hr>  
    <div class="table-responsive">
      <table class="table table-hover table-borderless">
        {% assign talks = site.data.talks  %}
      {% for item in talks %}
        <tr>
          <td>
           {{ item.title }}
          </td>
          <td>
           <a href="{{ item.page }}" target="_blank">{{ item.event }}</a>
          </td>
          <td  style="width: 15%"><strong>{{ item.date | date: "%m-%Y" }}</strong></td>
        </tr>
      {% endfor %}
      </table>
    </div>
</div>


<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid" src="{{ site.baseurl }}/assets/img/poster2.jpg" alt="" title=""/>
    </div>
</div>
<div class="caption">
    Presenting at the JINA Frontiers in Nuclear Astrophysics conference in South Bend, IN (2022).
</div>

<div class="news">  
   <h2>posters</h2>
  <hr>  
    <div class="table-responsive">
      <table class="table table-hover table-borderless">
        {% assign posters = site.data.posters  %}
      {% for item in posters %}
        <tr>
          <td>
           {{ item.title }}
          </td>
          <td>
          {% if item.figshare %}
           <a href="https://doi.org/{{ item.figshare }}" target="_blank"><i class="ai ai-figshare ai-2x"></i></a>
          {% endif %}
          </td>
          <td>
           <a href="{{ item.page }}" target="_blank">{{ item.event }}</a>
          </td>
          <td  style="width: 15%"><strong>{{ item.date | date: "%m-%Y" }}</strong></td>
          <!--
          <td><div class='altmetric-embed' data-badge-popover="left" data-link-target='_blank' data-hide-no-mentions="true" data-badge-type='donut' data-doi="{{ item.figshare }}"></div> </td>
          -->
          </tr>
      {% endfor %}
      </table>
    </div>
</div>
