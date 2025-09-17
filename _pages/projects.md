---
layout: page
title: projects
permalink: /projects/
description: what we are currently working on
nav: true
---

Below you can find a non-exhaustive list of projects our research group has been working on.

<div class="projects grid">

  {% assign sorted_projects = site.projects | sort: "importance" %}
  {% for project in sorted_projects %}
  <div class="grid-item">
    {% if project.redirect %}
    <a href="{{ project.redirect }}" target="_blank">
    {% else %}
    <a href="{{ project.url | relative_url }}">
    {% endif %}
      <div class="card hoverable">
        {% if project.img %}
        <img src="{{ project.img | relative_url }}" alt="project thumbnail">
        {% endif %}
        <div class="card-body">
          <h2 class="card-title">{{ project.title }}</h2>
          <p class="card-text">{{ project.description }}</p>
          <div class="row ml-1 mr-1 p-0">
            {% if project.github %}
            <div class="github-icon">
              <div class="icon" data-toggle="tooltip" title="Code Repository">
                <a href="{{ project.github }}" target="_blank"><i class="fab fa-github gh-icon"></i></a>
              </div>
              {% if project.github_stars %}
              <span class="stars" data-toggle="tooltip" title="GitHub Stars">
                <i class="fas fa-star"></i>
                <span id="{{ project.github_stars }}-stars"></span>
              </span>
              {% endif %}
            </div>
            {% endif %}
          </div>
        </div>
      </div>
    </a>
  </div>
{% endfor %}

</div>

<br>

## Frequently Asked Questions (FAQ)
<hr>

#### **Q: How can I get involved in nuclear astrophysics research at SMU?**

A: You are lucky that SMU has a few people working in nuclear astrophysics!
In addition to me, you can also work with [Prof. Christian](https://www.ap.smu.ca/~gchristian/) on experimental studies.

#### **Q: Are there opportunities for undergraduate students?**

A: Of course! There are many projects for students at all levels, from first-year to senior undergraduates.
You can also apply for Fellowships to partially support you (see below).

#### **Q: Do I need prior experience in nuclear physics or astrophysics?**

A: Not at all. A background in physics is helpful, but enthusiasm and a willingness to learn are most important.
We provide training in the necessary experimental and computational techniques.

#### **Q: What skills will I gain from working in your group?**

A: Depending on the project, you could learn experimental techniques at accelerator facilities, programming and data analysis (Python, C++), or computational modeling of astrophysical environments.

#### **Q: Are projects available during the summer or the academic year?**

A: Yes. We have opportunities for both summer research (often with fellowships) and part-time projects during the school year.

#### **Q: Do you collaborate with other universities or labs?**

A: Absolutely. Our group works with researchers at TRIUMF, RIKEN, FRIB, and other international facilities.
Students working in the group will have the opportunity to travel for experiments or meet our collaborators.

#### **Q: I have finished my Ph.D. and I am looking for a postdoc. Are there any positions available?**

A: I am currently not hiring postdocs, but if you are interested in any of the Fellowships below, I would be happy to support you
and your proposed project!

#### **Q: How should I contact you if I’m interested?**

A: Send me an [email](mailto:{{site.email}}) with a brief introduction, your background, and any particular interests.
Then we can then arrange a time to talk about potential projects.

## Research fellowships for students and postdocs
<hr>

### Undergraduate students

- [NSERC Undergraduate Student Research Awards](https://www.nserc-crsng.gc.ca/Students-Etudiants/UG-PC/USRA-BRPC_eng.asp) ($6,000 stipend for 16 weeks, in addition to at least another $4,000 and travel support)

- [CINP Undergraduate Research Scholarship](https://cinp.ca/cinp-undergraduate-research-scholarships-urs-2025-competition) ($6,000 stipend for 16 weeks, in addition to at least another $4,000 and travel support)

### Graduate students

- [NSERC Canada Graduate Research Scholarship (Ph.D)](https://www.nserc-crsng.gc.ca/Students-Etudiants/PG-CS/cgrsd-besrd_eng.asp)  ($40,000 per year for 3 years)

- [NSERC Canada Graduate Research Scholarship (M.Sc.)](https://www.nserc-crsng.gc.ca/Students-Etudiants/PG-CS/cgrsm-besrm_eng.asp)  ($27,000 for 12 months)

- [CINP Graduate Fellowship](https://cinp.ca/cinp-graduate-fellowship) ($15,000)

### Postdoctoral fellows

- [Japan Society for the Promotion of Science Postdoctoral Fellowships for Research in Japan (JSPS)](https://www.nserc-crsng.gc.ca/Students-Etudiants/PD-NP/JSPS_short-SJPS_court_eng.asp) (¥362,000 per month, round-trip air ticket, and ¥200,000 settling-in allowance)

- [Postdoctoral Fellowships - Marie Skłodowska-Curie Actions](https://marie-sklodowska-curie-actions.ec.europa.eu/actions/postdoctoral-fellowships)
