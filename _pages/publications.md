---
layout: page
permalink: /publications/
title: publications
description: our academic output
years: [2026, 2025, 2024, 2023, 2022, 2021, 2020, 2019, 2018, 2017, 2016]
nav: true
nav_order: 1
---

### overview
---


<i class="far fa-file-alt"></i> {% bibliography_count -f papers %} journal articles ({% bibliography_count -f papers --query @*[author^=Psaltis]%} leading)

[Phys. Rev. Lett.](https://prl.aps.org){:target="\_blank"}: {% bibliography_count -f papers --query @*[journal=Physical Review Letters]%} &nbsp; &middot; &nbsp; [Phys. Lett. B](https://www.sciencedirect.com/journal/physics-letters-b){:target="\_blank"}: {% bibliography_count -f papers --query @*[journal=Physics Letters B]%} &nbsp; &middot; &nbsp; [Phys. Rev. C](https://prc.aps.org){:target="\_blank"}: {% bibliography_count -f papers --query @*[journal=Physical Review C]%} &nbsp; &middot; &nbsp; [Astrophys. J](https://iopscience.iop.org/journal/0004-637X){:target="\_blank"}: {% bibliography_count -f papers --query @*[journal=The Astrophysical Journal]%}

<i class="far fa-file-alt"></i> {% bibliography_count -f proceedings %} conference proceedings articles ({% bibliography_count -f proceedings --query @*[author^=Psaltis]%} leading)


<svg id="publications-chart" viewBox="0 0 450 200" style="width: 100%; height: auto;" role="img" aria-label="Publications per year, split by journal articles and conference proceedings"></svg>

<script>

const publicationData = [
  {% assign chart_years = page.years | reverse %}
  {% for y in chart_years %}
  {
    group: "{{ y }}",
    "journal articles": {% bibliography_count -f papers --query @*[year={{ y }}]* %},
    "conference proceedings": {% bibliography_count -f proceedings --query @*[year={{ y }}]* %}
  }{% unless forloop.last %},{% endunless %}
  {% endfor %}
];

// Set the dimensions and margins of the graph
const margin = { top: 10, right: 30, bottom: 20, left: 50 },
      width = 460 - margin.left - margin.right,
      height = 200 - margin.top - margin.bottom;

// Append the svg object to the body of the page
const svg = d3.select("#publications-chart")
  .attr("width", width + margin.left + margin.right)
  .attr("height", height + margin.top + margin.bottom)
  .append("g")
  .attr("transform", `translate(${margin.left},${margin.top})`);

// Publication counts are generated from papers.bib and proceedings.bib at build time.
const data = publicationData;

  // List of subgroups
  const subgroups = ["journal articles", "conference proceedings"];

  // List of groups (species in this case)
  const groups = Array.from(new Set(data.map(d => d.group)));

  // Add X axis
  const x = d3.scaleBand()
    .domain(groups)
    .range([0, width])
    .padding(0.2);

  svg.append("g")
    .attr("transform", `translate(0,${height})`)
    .call(d3.axisBottom(x).tickSize(0))
    .selectAll("path, line")
    .style("opacity", 0); // Hide axis lines

  // Add Y axis
  const y = d3.scaleLinear()
  .domain([0, d3.max(data, d =>
  d3.sum(subgroups, key => +d[key])
  )+2])
    .range([height, 0]);

  svg.append("g")
    .call(d3.axisLeft(y).tickValues([0, 5, 10, 15, 20]).tickSize(0))
    .selectAll("path, line")
    .style("opacity", 0); // Hide axis lines

  // Color palette for each subgroup
  const color = d3.scaleOrdinal()
    .domain(subgroups)
    .range(['#9D2235','#E0E0E0']);

  // Stack the data per subgroup
  const stackedData = d3.stack()
    .keys(subgroups)(data);

  // Show the bars
  svg.append("g")
    .selectAll("g")
    .data(stackedData)
    .enter().append("g")
    .attr("fill", d => color(d.key))
    .selectAll("rect")
    .data(d => d)
    .enter().append("rect")
      .attr("x", d => x(d.data.group))
      .attr("y", d => y(d[1]))
      .attr("height", d => y(d[0]) - y(d[1]))
      .attr("width", x.bandwidth())
    // Add mouseover and mouseout events
    .on("mouseover", function(event, d) {
      d3.select(this).style("opacity", 0.7);

      // Show count label on hover
      const count = d[1] - d[0];
      svg.append("text")
        .attr("class", "count-label")
        .attr("x", x(d.data.group) + x.bandwidth() / 2)
        .attr("y", y(d[1]) - 5)
        .attr("text-anchor", "middle")
        .text(count);
    })
    .on("mouseout", function(event, d) {
      d3.select(this).style("opacity", 1); // Reset opacity

      // Remove count label on mouseout
      svg.selectAll(".count-label").remove();
    })
    .on("click", function(event, d) {
      const yearButton = document.querySelector('.year-chip[data-year="' + d.data.group + '"]');
      if (yearButton) yearButton.click();

      // Display count label permanently on click
      svg.selectAll(".click-label").remove();
      const count = d[1] - d[0];
      svg.append("text")
        .attr("class", "count-label click-label")
        .attr("x", x(d.data.group) + x.bandwidth() / 2)
        .attr("y", y(d[1]) - 5)
        .attr("text-anchor", "middle")
        .text(count);
    });

  // Create a legend
  const legend = svg.append("g")
    .attr("class", "legend")
    .attr("transform", `translate(${width - 370}, 10)`);

  // Add legend squares
  legend.selectAll("legend")
    .data(subgroups)
    .enter().append("rect")
    .attr("x", 0)
    .attr("y", (d, i) => i * 20) // Adjust vertical spacing
    .attr("width", 10)
    .attr("height", 10)
    .style("fill", color);

  // Add legend labels
  legend.selectAll("text")
    .data(subgroups)
    .enter().append("text")
    .attr("x", 20)
    .attr("y", (d, i) => i * 20 + 9) // Adjust vertical position
    .style("font-size", "12px")
    .text(d => d);

</script>

<br>


<section class="publication-browser" aria-label="Publication browser">
  <div class="publication-controls">
    <label for="year-select">Year</label>
    <select id="year-select">
      {% for y in page.years %}
      <option value="{{ y }}">{{ y }}</option>
      {% endfor %}
    </select>

    <div class="year-buttons" aria-label="Publication years">
      {% for y in page.years %}
      <button type="button" class="year-chip" data-year="{{ y }}">{{ y }}</button>
      {% endfor %}
    </div>
  </div>

  <div class="tag-filter" aria-label="Publication tags">
    <button type="button" class="tag-chip active" data-tag="all" aria-pressed="true">All</button>
    <button type="button" class="tag-chip" data-tag="experimental" aria-pressed="false">Experimental</button>
    <button type="button" class="tag-chip" data-tag="nucleosynthesis" aria-pressed="false">Nucleosynthesis</button>
    <button type="button" class="tag-chip" data-tag="reaction-rates" aria-pressed="false">Reaction rates</button>
    <button type="button" class="tag-chip" data-tag="x-ray-bursts" aria-pressed="false">X-ray bursts</button>
    <button type="button" class="tag-chip" data-tag="classical-nova" aria-pressed="false">Classical nova</button>
    <button type="button" class="tag-chip" data-tag="supernova" aria-pressed="false">Supernova</button>
    <button type="button" class="tag-chip" data-tag="theory" aria-pressed="false">Theory</button>
    <button type="button" class="tag-chip" data-tag="observational" aria-pressed="false">Observational</button>
  </div>

  <div id="publication-status" class="publication-status" role="status" aria-live="polite"></div>
  <div id="publications-list" data-base-url="{{ site.baseurl }}"></div>
</section>

<script>
  document.addEventListener('DOMContentLoaded', function() {
    const years = {{ page.years | jsonify }};
    const cache = {};
    let activeYear = String(years[0]);
    let activeTag = 'all';

    const tagRules = {
      experimental: ['experiment', 'measurement', 'cross section', 'beam', 'detector', 'recoil separator', 'spectroscopy', 'activation'],
      nucleosynthesis: ['nucleosynthesis', 'abundance', 'abundances'],
      'reaction-rates': ['reaction rate', 'reaction rates', 'thermonuclear', 'rate uncertainty', 'monte carlo rate'],
      'x-ray-bursts': ['x-ray burst', 'x-ray bursts', 'xrbs', 'type-i x-ray', 'accreting neutron'],
      'classical nova': ['classical novae', 'nova explosions'],
      supernovae: ['supernova', 'supernovae', 'core-collapse', 'ccsne', 'neutrino-driven'],
      theory: [ 'simulation', 'simulations', 'bayesian', 'network', 'sensitivity study'],
      observational:['lines', 'stars', 'observation']
    };

    const tagLabels = {
      experimental: 'Experimental',
      nucleosynthesis: 'Nucleosynthesis',
      'reaction-rates': 'Reaction rates',
      'x-ray-bursts': 'X-ray bursts',
      'classical nova': 'Classical nova',
      supernovae: 'Supernova',
      theory: 'Theory',
      observational: 'Observational'
    };

    const yearSelect = document.getElementById('year-select');
    const yearButtons = document.querySelectorAll('.year-chip');
    const tagButtons = document.querySelectorAll('.tag-chip');
    const list = document.getElementById('publications-list');
    const status = document.getElementById('publication-status');
    const baseUrl = list.dataset.baseUrl || '';
    const loadedScripts = {};

    function publicationUrl(year) {
      return `${baseUrl}/publications/years/${year}/`;
    }

    function setStatus(message) {
      status.textContent = message;
    }

    function setActiveYear(year) {
      activeYear = String(year);
      yearSelect.value = activeYear;
      yearButtons.forEach(function(button) {
        const selected = button.dataset.year === activeYear;
        button.classList.toggle('active', selected);
        button.setAttribute('aria-pressed', selected ? 'true' : 'false');
      });
    }

    function setActiveTag(tag) {
      activeTag = tag;
      tagButtons.forEach(function(button) {
        const selected = button.dataset.tag === activeTag;
        button.classList.toggle('active', selected);
        button.setAttribute('aria-pressed', selected ? 'true' : 'false');
      });
      filterPublications();
    }

    function tagsForPublication(item) {
      const text = item.textContent.toLowerCase();
      return Object.keys(tagRules).filter(function(tag) {
        return tagRules[tag].some(function(term) {
          return text.includes(term);
        });
      });
    }

    function decoratePublications() {
      list.querySelectorAll('ol.bibliography > li').forEach(function(item) {
        if (item.dataset.tagsReady) return;

        const tags = tagsForPublication(item);
        item.dataset.tags = tags.join(' ');
        item.dataset.tagsReady = 'true';

        if (tags.length) {
          const tagList = document.createElement('div');
          tagList.className = 'publication-tags';
          tags.forEach(function(tag) {
            const badge = document.createElement('span');
            badge.className = 'publication-tag';
            badge.textContent = tagLabels[tag];
            tagList.appendChild(badge);
          });
          item.appendChild(tagList);
        }
      });
    }

    function bindBibliographyToggles() {
      if (!window.jQuery) return;
      const $items = $('#publications-list a.abstract, #publications-list a.bibtex');
      $items.off('click.publicationBrowser').on('click.publicationBrowser', function() {
        const target = $(this).hasClass('abstract') ? '.abstract.hidden' : '.bibtex.hidden';
        $(this).parent().parent().find(target).toggleClass('open');
      });
    }

    function loadScriptOnce(src, callback) {
      if (loadedScripts[src]) {
        if (callback) callback();
        return;
      }

      const script = document.createElement('script');
      script.src = src;
      script.async = true;
      script.onload = function() {
        loadedScripts[src] = true;
        if (callback) callback();
      };
      document.head.appendChild(script);
    }

    function refreshPublicationBadges() {
      loadScriptOnce('https://d1bxh8uas1mnw7.cloudfront.net/assets/embed.js', function() {
        if (window._altmetric_embed_init) window._altmetric_embed_init();
      });

      loadScriptOnce('https://badge.dimensions.ai/badge.js', function() {
        if (window.__dimensions_embed && window.__dimensions_embed.addBadges) {
          window.__dimensions_embed.addBadges();
        }
      });
    }

    function filterPublications() {
      const items = list.querySelectorAll('ol.bibliography > li');
      let visible = 0;

      items.forEach(function(item) {
        const show = activeTag === 'all' || item.dataset.tags.split(' ').includes(activeTag);
        item.hidden = !show;
        if (show) visible += 1;
      });

      if (items.length) {
        setStatus(activeTag === 'all'
          ? `Showing ${items.length} publication${items.length === 1 ? '' : 's'} from ${activeYear}`
          : `Showing ${visible} ${tagLabels[activeTag].toLowerCase()} publication${visible === 1 ? '' : 's'} from ${activeYear}`);
      }
    }

    function showYear(year) {
      setActiveYear(year);
      if (cache[activeYear]) {
        list.innerHTML = cache[activeYear];
        decoratePublications();
        bindBibliographyToggles();
        refreshPublicationBadges();
        filterPublications();
        return;
      }

      list.innerHTML = '';
      setStatus(`Loading ${activeYear} publications...`);

      fetch(publicationUrl(activeYear))
        .then(function(response) {
          if (!response.ok) throw new Error('Could not load publications');
          return response.text();
        })
        .then(function(html) {
          cache[activeYear] = html;
          list.innerHTML = html;
          decoratePublications();
          bindBibliographyToggles();
          refreshPublicationBadges();
          filterPublications();
        })
        .catch(function() {
          setStatus(`Sorry, the ${activeYear} publications could not be loaded.`);
        });
    }

    yearSelect.addEventListener('change', function() {
      showYear(this.value);
    });

    yearButtons.forEach(function(button) {
      button.addEventListener('click', function() {
        showYear(this.dataset.year);
      });
    });

    tagButtons.forEach(function(button) {
      button.addEventListener('click', function() {
        setActiveTag(this.dataset.tag);
      });
    });

    showYear(activeYear);
  });
</script>
