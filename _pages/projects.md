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

<div class="accordion" id="accordionExample">
  <div class="card">
    <div class="card-header" id="headingOne">
      <h2 class="mb-0">
        <button class="btn btn-link btn-block text-left collapsed larger-font no-uppercase" type="button" data-toggle="collapse" data-target="#collapseOne" aria-expanded="false" aria-controls="collapseOne" >
        How can I get involved in nuclear astrophysics research at SMU?
        </button>
      </h2>
    </div>

    <div id="collapseOne" class="collapse" aria-labelledby="headingOne" data-parent="#accordionExample">
      <div class="card-body">
      You are lucky that SMU has a few people working in nuclear astrophysics!
      In addition to me, you can also work with <a href="https://www.ap.smu.ca/~gchristian/">Prof. Christian</a> on experimental studies.
      </div>
    </div>
  </div>
  <div class="card">
    <div class="card-header" id="headingTwo">
      <h2 class="mb-0">
        <button class="btn btn-link btn-block text-left collapsed larger-font no-uppercase" type="button" data-toggle="collapse" data-target="#collapseTwo" aria-expanded="false" aria-controls="collapseTwo" >
         Are there opportunities for undergraduate students?
        </button>
      </h2>
    </div>
    <div id="collapseTwo" class="collapse" aria-labelledby="headingTwo" data-parent="#accordionExample">
      <div class="card-body">
      Of course! There are many projects for students at all levels, from first-year to senior undergraduates.
      You can also apply for Fellowships to partially support you (see below).
      </div>
    </div>
  </div>
  <div class="card">
    <div class="card-header" id="headingThree">
      <h2 class="mb-0">
        <button class="btn btn-link btn-block text-left collapsed larger-font no-uppercase" type="button" data-toggle="collapse" data-target="#collapseThree" aria-expanded="false" aria-controls="collapseThree">
          Do I need prior experience in nuclear physics or astrophysics?
        </button>
      </h2>
    </div>
    <div id="collapseThree" class="collapse" aria-labelledby="headingThree" data-parent="#accordionExample">
      <div class="card-body">
        Not at all. A background in physics is helpful, but enthusiasm and a willingness to learn are most important. We provide training in the necessary experimental and computational techniques.
      </div>
    </div>
  </div>
  <div class="card">
    <div class="card-header" id="headingFour">
      <h2 class="mb-0">
        <button class="btn btn-link btn-block text-left collapsed larger-font no-uppercase" type="button" data-toggle="collapse" data-target="#collapseFour" aria-expanded="false" aria-controls="collapseFour" >
          What skills will I gain from working in your group?
        </button>
      </h2>
    </div>
    <div id="collapseFour" class="collapse" aria-labelledby="headingFour" data-parent="#accordionExample">
      <div class="card-body">
        Depending on the project, you could learn experimental techniques at accelerator facilities, programming and data analysis (Python, C++), or computational modeling of astrophysical environments.
      </div>
    </div>
  </div>
  <div class="card">
    <div class="card-header" id="headingFive">
      <h2 class="mb-0">
        <button class="btn btn-link btn-block text-left collapsed larger-font no-uppercase" type="button" data-toggle="collapse" data-target="#collapseFive" aria-expanded="false" aria-controls="collapseFive" >
       Are projects available during the summer or the academic year?
        </button>
      </h2>
    </div>
    <div id="collapseFive" class="collapse" aria-labelledby="headingFive" data-parent="#accordionExample">
      <div class="card-body">
        Yes. We have opportunities for both summer research (often with fellowships) and part-time projects during the school year.
      </div>
    </div>
  </div>
  <div class="card">
    <div class="card-header" id="headingSix">
      <h2 class="mb-0">
        <button class="btn btn-link btn-block text-left collapsed larger-font no-uppercase" type="button" data-toggle="collapse" data-target="#collapseSix" aria-expanded="false" aria-controls="collapseSix" >
        Do you collaborate with other universities or labs?
        </button>
      </h2>
    </div>
    <div id="collapseSix" class="collapse" aria-labelledby="headingSix" data-parent="#accordionExample">
      <div class="card-body">
        Absolutely. Our group works with researchers at TRIUMF (Vancouver), RIKEN (Japan), FRIB (USA), and other international facilities. Students working in the group will have the opportunity to travel for experiments or meet our collaborators.
      </div>
    </div>
  </div>
  <div class="card">
    <div class="card-header" id="headingSeven">
      <h2 class="mb-0">
        <button class="btn btn-link btn-block text-left collapsed larger-font no-uppercase" type="button" data-toggle="collapse" data-target="#collapseSeven" aria-expanded="false" aria-controls="collapseSeven" >
        I have finished my Ph.D. and I am looking for a postdoc. Are there any positions available?
        </button>
      </h2>
    </div>
    <div id="collapseSeven" class="collapse" aria-labelledby="headingSeven" data-parent="#accordionExample">
      <div class="card-body">
        I am currently not hiring postdocs, but if you are interested in any of the Fellowships below, I would be happy to support you and your proposed project!
      </div>
    </div>
  </div>
  <div class="card">
    <div class="card-header" id="headingEight">
      <h2 class="mb-0">
        <button class="btn btn-link btn-block text-left collapsed larger-font no-uppercase" type="button" data-toggle="collapse" data-target="#collapseEight" aria-expanded="false" aria-controls="collapseEight" >
        How should I contact you if I’m interested?
        </button>
      </h2>
    </div>
    <div id="collapseEight" class="collapse" aria-labelledby="headingEight" data-parent="#accordionExample">
      <div class="card-body">
        Send me an <a href="mailto:thanassis.psaltis@smu.ca">email</a> with a brief introduction, your background, and any particular interests. Then we can then arrange a time to talk about potential projects.
      </div>
    </div>
  </div>
</div>

<br>

## Research fellowships for students and postdocs
<hr>

### Undergraduate students


- [CINP Undergraduate Research Scholarship](https://cinp.ca/cinp-undergraduate-research-scholarships-urs-2025-competition) ($6,000 stipend for 16 weeks, in addition to at least another $4,000 and travel support)

- [NSERC Undergraduate Student Research Awards](https://www.nserc-crsng.gc.ca/Students-Etudiants/UG-PC/USRA-BRPC_eng.asp) ($6,000 stipend for 16 weeks, in addition to at least another $4,000 and travel support)

- [Dean of Science Summer Research Awards](https://www.smu.ca/research/student-research-opportunities.html) ($8,600 for 12 weeks)

- [First-Year Undergraduate Research Awards](https://www.smu.ca/research/student-research-opportunities.html) ($6,700 for 12 weeks)

For the last three awards, the application deadline is **February 20, 2026**.
If you are interested in working with the group, feel free to [contact](mailto:{{site.email}}) in advance.


### Graduate students

- [NSERC Canada Graduate Research Scholarship (Ph.D)](https://www.nserc-crsng.gc.ca/Students-Etudiants/PG-CS/cgrsd-besrd_eng.asp)  ($40,000 per year for 3 years)

- [NSERC Canada Graduate Research Scholarship (M.Sc.)](https://www.nserc-crsng.gc.ca/Students-Etudiants/PG-CS/cgrsm-besrm_eng.asp)  ($27,000 for 12 months)

- [CINP Graduate Fellowship](https://cinp.ca/cinp-graduate-fellowship) ($15,000)

- [Mitacs Globalink Research
  Award](https://www.mitacs.ca/our-programs/globalink-research-award/) ($6,000-$12,000
  for a 12-48 week internships abroad or at SMU

- [Durland Scholarships in Graduate Research](https://www.smu.ca/durlandscholarships/index.html) ($10,000 for M.Sc. and $15,000 for Ph.D.)
  This is a SMU entrance renewable (for 2 and 3 years respectively) designed to attract top research students.

### Postdoctoral fellows

- [Japan Society for the Promotion of Science Postdoctoral Fellowships for Research in Japan (JSPS)](https://www.nserc-crsng.gc.ca/Students-Etudiants/PD-NP/JSPS_short-SJPS_court_eng.asp) (¥362,000 per month, round-trip air ticket, and ¥200,000 settling-in allowance)

- [Postdoctoral Fellowships - Marie Skłodowska-Curie Actions](https://marie-sklodowska-curie-actions.ec.europa.eu/actions/postdoctoral-fellowships)

- [Postdoctoral Fellowships - Canadian Institute for Theoretical Astrophysics](https://www.cita.utoronto.ca/opportunities/post-docs/) ($80,000 per year)

- [Mitacs Globalink Research Award](https://www.mitacs.ca/our-programs/globalink-research-award/) ($6,000-$12,000 for a 12-48 week internships abroad or at SMU)
