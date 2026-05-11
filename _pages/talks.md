---
layout: page
permalink: /talks/
title: presentations
description:
nav: true
years: [2026, 2025, 2024, 2023, 2022, 2021, 2020, 2019, 2018, 2017, 2016, 2015, 2014, 2012]
---

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid" src="{{ site.baseurl }}/assets/img/nic_korea.JPG" alt="Thanassis presenting at Nuclei in the Cosmos in Daejeon, South Korea" title=""/>
    </div>
</div>
<div class="caption">
    Thanassis presenting at the 17th International Symposium on Nuclei in the Cosmos in Daejeon, South Korea (2023).
</div>

### overview
---
{% assign talks = site.data.talks %}
{% assign posters = site.data.posters %}
{% assign invited_talks = talks | where: "type", "invited" %}
{% assign invited_posters = posters | where: "type", "invited" %}
{% assign total = talks.size | plus: posters.size %}
{% assign total_invited = invited_talks.size | plus: invited_posters.size %}
{% assign recording_count = 0 %}
{% assign figshare_count = 0 %}
{% for item in talks %}
  {% if item.video %}
    {% assign recording_count = recording_count | plus: 1 %}
  {% endif %}
  {% if item.slides %}
    {% assign slides_count = slides_count | plus: 1 %}
  {% endif %}
{% endfor %}
{% for item in posters %}
  {% if item.figshare %}
    {% assign figshare_count = figshare_count | plus: 1 %}
  {% endif %}
{% endfor %}

<section class="presentation-browser" aria-label="Presentation browser">
  <div class="presentation-summary" aria-label="Presentation summary">
    <div><strong>{{ total }}</strong><span>presentations</span></div>
    <div><strong>{{ total_invited }}</strong><span>invited</span></div>
    <div><strong id="presentation-countries-count">...</strong><span>countries</span></div>
    <div><strong>{{ recording_count }}</strong><span>recordings</span></div>
    <div><strong>{{ figshare_count }}</strong><span>figshare posters</span></div>
  </div>

  <div class="presentation-controls">
    <label for="presentation-year">Year</label>
    <select id="presentation-year">
      <option value="all">All years</option>
      {% for y in page.years %}
      <option value="{{ y }}">{{ y }}</option>
      {% endfor %}
    </select>

    <label for="presentation-search">Search</label>
    <input id="presentation-search" type="search" placeholder="Title, event, place..." autocomplete="off">
  </div>

  <div class="presentation-filter" aria-label="Presentation format">
    <button type="button" class="presentation-chip active" data-filter-group="format" data-filter-value="all" aria-pressed="true">All</button>
    <button type="button" class="presentation-chip" data-filter-group="format" data-filter-value="talk" aria-pressed="false">Talks</button>
    <button type="button" class="presentation-chip" data-filter-group="format" data-filter-value="poster" aria-pressed="false">Posters</button>
  </div>

  <div class="presentation-filter" aria-label="Presentation type">
    <button type="button" class="presentation-chip active" data-filter-group="kind" data-filter-value="all" aria-pressed="true">All types</button>
    <button type="button" class="presentation-chip" data-filter-group="kind" data-filter-value="invited" aria-pressed="false">Invited</button>
    <button type="button" class="presentation-chip" data-filter-group="kind" data-filter-value="contributed" aria-pressed="false">Contributed</button>
  </div>

  <div class="presentation-filter" aria-label="Presentation media">
    <button type="button" class="presentation-chip active" data-filter-group="media" data-filter-value="all" aria-pressed="true">All media</button>
    <button type="button" class="presentation-chip" data-filter-group="media" data-filter-value="video" aria-pressed="false"><i class="fa fa-video"></i> Recording</button>
    <button type="button" class="presentation-chip" data-filter-group="media" data-filter-value="figshare" aria-pressed="false"><i class="ai ai-figshare"></i> Figshare</button>
  </div>

  <div id="presentation-status" class="presentation-status" role="status" aria-live="polite"></div>

  <div class="table-responsive">
    <table class="table table-hover table-borderless presentation-table">
      <thead>
        <tr>
          <th scope="col">Date</th>
          <th scope="col">Presentation</th>
          <th scope="col">Event</th>
          <th scope="col">Links</th>
        </tr>
      </thead>
      <tbody id="presentation-list">
        {% for item in talks %}
        {% assign presentation_kind = "contributed" %}
        {% if item.type == "invited" %}
          {% assign presentation_kind = "invited" %}
        {% endif %}
        <tr class="presentation-item"
            data-date="{{ item.date | date: '%Y-%m' }}"
            data-year="{{ item.date | date: '%Y' }}"
            data-format="talk"
            data-kind="{{ presentation_kind }}"
            data-media="{% if item.video %} video{% endif %}{% if item.slides %} slides{% endif %}"
            data-event="{{ item.event | escape }}"
            data-search="{{ item.title | append: ' ' | append: item.event | downcase | escape }}">
          <td class="presentation-date"><strong>{{ item.date | date: "%m-%Y" }}</strong></td>
          <td>
            <span class="presentation-badge">Talk</span>
            {% if presentation_kind == "invited" %}
            <span class="presentation-badge invited">Invited</span>
            {% endif %}
            <div class="presentation-title">{{ item.title }}</div>
          </td>
          <td>
            {% if item.page %}
            <a href="{{ item.page }}" target="_blank">{{ item.event }}</a>
            {% else %}
            {{ item.event }}
            {% endif %}
          </td>
          <td class="presentation-links">
            {% if item.slides %}
            <a href="{{ site.baseurl }}/assets/talks/{{ item.slides }}" target="_blank" aria-label="Slides for {{ item.title }}"><i class="fa fa-desktop"></i></a>
            {% endif %}
            {% if item.video %}
            <a href="{{ item.video }}" target="_blank" aria-label="Recording for {{ item.title }}"><i class="fa fa-video"></i></a>
            {% endif %}
          </td>
        </tr>
        {% endfor %}
        {% for item in posters %}
        {% assign presentation_kind = "contributed" %}
        {% if item.type == "invited" %}
          {% assign presentation_kind = "invited" %}
        {% endif %}
        <tr class="presentation-item"
            data-date="{{ item.date | date: '%Y-%m' }}"
            data-year="{{ item.date | date: '%Y' }}"
            data-format="poster"
            data-kind="{{ presentation_kind }}"
            data-media="{% if item.figshare %} figshare{% endif %}"
            data-event="{{ item.event | escape }}"
            data-search="{{ item.title | append: ' ' | append: item.event | downcase | escape }}">
          <td class="presentation-date"><strong>{{ item.date | date: "%m-%Y" }}</strong></td>
          <td>
            <span class="presentation-badge">Poster</span>
            {% if presentation_kind == "invited" %}
            <span class="presentation-badge invited">Invited</span>
            {% endif %}
            <div class="presentation-title">{{ item.title }}</div>
          </td>
          <td>
            {% if item.page %}
            <a href="{{ item.page }}" target="_blank">{{ item.event }}</a>
            {% else %}
            {{ item.event }}
            {% endif %}
          </td>
          <td class="presentation-links">
            {% if item.figshare %}
            <a href="https://doi.org/{{ item.figshare }}" target="_blank" aria-label="Figshare poster for {{ item.title }}"><i class="ai ai-figshare ai-2x"></i></a>
            {% endif %}
          </td>
        </tr>
        {% endfor %}
      </tbody>
    </table>
  </div>
</section>

<script>
  document.addEventListener('DOMContentLoaded', function() {
    const filters = {
      year: 'all',
      format: 'all',
      kind: 'all',
      media: 'all',
      query: ''
    };

    const yearSelect = document.getElementById('presentation-year');
    const searchInput = document.getElementById('presentation-search');
    const status = document.getElementById('presentation-status');
    const countriesCount = document.getElementById('presentation-countries-count');
    const list = document.getElementById('presentation-list');
    const rows = Array.from(list.querySelectorAll('.presentation-item'));
    const countryAliases = {
      'bc': 'Canada',
      'ca': 'USA',
      'catalonia': 'Spain',
      'hi': 'USA',
      'in': 'USA',
      'mi': 'USA',
      'nh': 'USA',
      'ns': 'Canada',
      'on': 'Canada',
      'usa': 'USA',
      'united states': 'USA'
    };

    rows.sort(function(a, b) {
      return b.dataset.date.localeCompare(a.dataset.date);
    }).forEach(function(row) {
      list.appendChild(row);
    });

    function matches(row) {
      const media = row.dataset.media.trim().split(/\s+/).filter(Boolean);
      const queryMatch = !filters.query || row.dataset.search.includes(filters.query);

      return (filters.year === 'all' || row.dataset.year === filters.year)
        && (filters.format === 'all' || row.dataset.format === filters.format)
        && (filters.kind === 'all' || row.dataset.kind === filters.kind)
        && (filters.media === 'all' || media.includes(filters.media))
        && queryMatch;
    }

    function updateStatus(visible) {
      status.textContent = `Showing ${visible} presentation${visible === 1 ? '' : 's'}`;
    }

    function countryFromEvent(eventName) {
      const locationMatch = eventName.match(/\(([^()]*)\)\s*$/);
      if (!locationMatch) return null;

      const location = locationMatch[1].trim();
      if (!location || location.toLowerCase() === 'virtually') return null;

      const parts = location.split(',').map(function(part) {
        return part.trim();
      }).filter(Boolean);
      const country = parts[parts.length - 1];

      return countryAliases[country.toLowerCase()] || country;
    }

    function updateCountryCount() {
      const countries = new Set();

      rows.forEach(function(row) {
        const country = countryFromEvent(row.dataset.event);
        if (country) countries.add(country);
      });

      countriesCount.textContent = countries.size;
    }

    function applyFilters() {
      let visible = 0;

      rows.forEach(function(row) {
        const show = matches(row);
        row.hidden = !show;
        if (show) visible += 1;
      });

      updateStatus(visible);
    }

    yearSelect.addEventListener('change', function() {
      filters.year = this.value;
      applyFilters();
    });

    searchInput.addEventListener('input', function() {
      filters.query = this.value.trim().toLowerCase();
      applyFilters();
    });

    document.querySelectorAll('.presentation-chip').forEach(function(button) {
      button.addEventListener('click', function() {
        const group = this.dataset.filterGroup;
        filters[group] = this.dataset.filterValue;

        document.querySelectorAll('.presentation-chip[data-filter-group="' + group + '"]').forEach(function(chip) {
          const selected = chip === button;
          chip.classList.toggle('active', selected);
          chip.setAttribute('aria-pressed', selected ? 'true' : 'false');
        });

        applyFilters();
      });
    });

    applyFilters();
    updateCountryCount();
  });
</script>
