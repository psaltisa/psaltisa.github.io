---
layout: page
permalink: /publications/
title: publications
description: my academic output
years: [2022, 2021, 2020, 2019, 2018, 2017, 2016]
nav: true
---

### Overview
---
<i class="far fa-file-alt"></i> {% bibliography_count -f papers %} journal articles ({% bibliography_count -f papers --query @*[author^=Psaltis]%} first author)

[Phys. Rev. Lett.](https://prl.aps.org){:target="\_blank"}: {% bibliography_count -f papers --query @*[journal=Physical Review Letters]%} &nbsp; &middot; &nbsp; [Phys. Lett. B](https://prl.aps.org){:target="\_blank"}: {% bibliography_count -f papers --query @*[journal=Physics Letters B]%} &nbsp; &middot; &nbsp; [Phys. Rev. C](https://prc.aps.org){:target="\_blank"}: {% bibliography_count -f papers --query @*[journal=Physical Review C]%} &nbsp; &middot; &nbsp; [Astrophys. J](https://iopscience.iop.org/journal/0004-637X){:target="\_blank"}: {% bibliography_count -f papers --query @*[journal=Astrophysical Journal]%}

<i class="far fa-file-alt"></i> {% bibliography_count -f proceedings %} conference proceedings articles ({% bibliography_count -f proceedings --query @*[author^=Psaltis]%} first author)

<i class="fas fa-book"></i> <a href="https://macsphere.mcmaster.ca/handle/11375/25859" target="_blank" >Ph.D. Thesis</a> &nbsp; &middot; &nbsp; <i class="fas fa-book"></i> <a href="https://doi.org/10.6084/m9.figshare.1257763.v2" target="_blank" >B.Sc. Thesis (in Greek)</a>

---

<div class="publications">
<h3>Journal Articles</h3>
{% for y in page.years %}
    {% if y!= 2018 %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f papers -q @*[year={{y}}]* %}
    {% endif %}
{% endfor %}
</div>

<br><br>


<div class="publications">
<h3>Articles in Conference Proceedings</h3>
{% for y in page.years %}
     {% if y!= 2016 and y!=2021 and y!=2022 %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f proceedings -q @*[year={{y}}]* %}
     {% endif %}
{% endfor %}
</div>
