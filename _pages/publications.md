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


<svg viewBox="0 0 450 200" style="width: 100%; height: auto;"></svg>

<script>

// Set the dimensions and margins of the graph
const margin = { top: 10, right: 30, bottom: 20, left: 50 },
      width = 460 - margin.left - margin.right,
      height = 200 - margin.top - margin.bottom;

// Append the svg object to the body of the page
const svg = d3.select("svg")
  .attr("width", width + margin.left + margin.right)
  .attr("height", height + margin.top + margin.bottom)
  .append("g")
  .attr("transform", `translate(${margin.left},${margin.top})`);

// Parse the Data (assuming you’re loading it from a CSV)
d3.csv("{{ site.baseurl }}/assets/csv/data_publications.csv").then(function(data) {

  // List of subgroups (columns in the CSV except for the first one)
  const subgroups = data.columns.slice(1);

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
    .domain([0, 20])
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
      // Display count label permanently on click
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

}).catch(function(error) {
  console.error('Error loading the CSV data:', error);
});

</script>

<br>


<!-- Dropdown for selecting year -->
<div>
  <label for="year-select">Select a year:</label>
  <select id="year-select">
    <option value="">--Select Year--</option>
    {% for y in page.years %}
    <option value="{{ y }}">{{ y }}</option>
    {% endfor %}
  </select>
</div>

<!-- Render all publications but hide them initially -->
<div id="publications-list">
  {% for y in page.years %}
  <div class="publications" data-year="{{ y }}" style="display: none;">
    <h3>Journal Articles ({{ y }})</h3>
    {% bibliography -f papers -q @*[year={{y}}]* %}

    <h3>Conference Proceedings ({{ y }})</h3>
    {% bibliography -f proceedings -q @*[year={{y}}]* %}
  </div>
  {% endfor %}
</div>

<script>
  document.addEventListener('DOMContentLoaded', function() {
    var yearSelect = document.getElementById('year-select');
    var latestYear = yearSelect.options[1].value; // Select the first option after the placeholder
    yearSelect.value = latestYear;

    // Trigger change event to display the latest year's publications
    var event = new Event('change');
    yearSelect.dispatchEvent(event);
  });

  document.getElementById('year-select').addEventListener('change', function() {
    var selectedYear = this.value;

    // Hide all publication divs
    var publicationDivs = document.querySelectorAll('#publications-list .publications');
    publicationDivs.forEach(function(div) {
      div.style.display = 'none';
    });

    // Show the selected year's publications
    if (selectedYear) {
      var selectedDiv = document.querySelector('#publications-list .publications[data-year="' + selectedYear + '"]');
      if (selectedDiv) {
        selectedDiv.style.display = 'block';
      }
    }
  });
</script>
