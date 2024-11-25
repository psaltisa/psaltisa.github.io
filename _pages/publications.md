---
layout: page
permalink: /publications/
title: publications
description: my academic output
years: [2024, 2023, 2022, 2021, 2020, 2019, 2018, 2017, 2016]
nav: true
nav_order: 1
---

### overview
---
<i class="far fa-file-alt"></i> {% bibliography_count -f papers %} journal articles ({% bibliography_count -f papers --query @*[author^=Psaltis]%} first author)

[Phys. Rev. Lett.](https://prl.aps.org){:target="\_blank"}: {% bibliography_count -f papers --query @*[journal=Physical Review Letters]%} &nbsp; &middot; &nbsp; [Phys. Lett. B](https://www.sciencedirect.com/journal/physics-letters-b){:target="\_blank"}: {% bibliography_count -f papers --query @*[journal=Physics Letters B]%} &nbsp; &middot; &nbsp; [Phys. Rev. C](https://prc.aps.org){:target="\_blank"}: {% bibliography_count -f papers --query @*[journal=Physical Review C]%} &nbsp; &middot; &nbsp; [Astrophys. J](https://iopscience.iop.org/journal/0004-637X){:target="\_blank"}: {% bibliography_count -f papers --query @*[journal=The Astrophysical Journal]%}

<i class="far fa-file-alt"></i> {% bibliography_count -f proceedings %} conference proceedings articles ({% bibliography_count -f proceedings --query @*[author^=Psaltis]%} first author)

<i class="fas fa-book"></i> <a href="https://macsphere.mcmaster.ca/handle/11375/25859" target="_blank" >Ph.D. Thesis</a> &nbsp; &middot; &nbsp; <i class="fas fa-book"></i> <a href="https://doi.org/10.6084/m9.figshare.1257763.v2" target="_blank" >B.Sc. Thesis (in Greek)</a>

<br>

<svg viewBox="0 0 450 200"></svg>


<script align="center">

// set the dimensions and margins of the graph
var margin = {top: 10, right: 30, bottom: 20, left: 50},
    width = 460 - margin.left - margin.right,
    height = 200 - margin.top - margin.bottom;

// append the svg object to the body of the page
var svg = d3.select("svg")
  .append("svg")
    .attr("width", width + margin.left + margin.right)
    .attr("height", height + margin.top + margin.bottom)
  .append("g")
    .attr("transform",
          "translate(" + margin.left + "," + margin.top + ")");

// Parse the Data
d3.csv("{{ site.baseurl }}/assets/csv/data_publications.csv", function(data) {

  // List of subgroups = header of the csv files = soil condition here
  var subgroups = data.columns.slice(1)

  // List of groups = species here = value of the first column called group -> I show them on the X axis
  var groups = d3.map(data, function(d){return(d.group)}).keys()

  // Add X axis
  var x = d3.scaleBand()
      .domain(groups)
      .range([0, width])
      .padding([0.2])
  svg.append("g")
    .attr("transform", "translate(0," + height + ")")
    .call(d3.axisBottom(x).tickSize(0))
    .selectAll("path, line")
    .style("opacity", 0.0); // Adjust the opacity value



  // Add Y axis
  var y = d3.scaleLinear()
    .domain([0, 20])
    .range([ height, 0 ]);
  svg.append("g")
    .call(d3.axisLeft(y).tickValues([0, 5, 10, 15, 20]).tickSize(0))
    .selectAll("path, line")
    .style("opacity", 0.0); // Adjust the opacity value

  // color palette = one color per subgroup
  var color = d3.scaleOrdinal()
    .domain(subgroups)
    .range(['#cc0000','#E0E0E0'])

  //stack the data? --> stack per subgroup
  var stackedData = d3.stack()
    .keys(subgroups)
    (data)

  // Show the bars
  svg.append("g")
    .selectAll("g")
    // Enter in the stack data = loop key per key = group per group
    .data(stackedData)
    .enter().append("g")
      .attr("fill", function(d) { return color(d.key); })
      .selectAll("rect")
      // enter a second time = loop subgroup per subgroup to add all rectangles
      .data(function(d) { return d; })
      .enter().append("rect")
        .attr("x", function(d) { return x(d.data.group); })
        .attr("y", function(d) { return y(d[1]); })
        .attr("height", function(d) { return y(d[0]) - y(d[1]); })
        .attr("width",x.bandwidth())
      // Add mouseover and mouseout events
        .on("mouseover", function(d) {
          d3.select(this)
            .style("opacity", 0.7); // Adjust opacity or add other effects
          // You can also show tooltips or other information here

        // Show count label
          var count = d[1] - d[0];
          svg.append("text")
            .attr("class", "count-label")
            .attr("x", x(d.data.group) + x.bandwidth() / 2)
            .attr("y", y(d[1]) - 5)
            .attr("text-anchor", "middle")
            .text(count);
          })
        .on("mouseout", function(d) {
          d3.select(this)
            .style("opacity", 1); // Reset to full opacity
          // You can hide tooltips or reset other changes here
          // Remove count label
          svg.selectAll(".count-label").remove();
          })
        .on("click", function(d) {
        // Display count label permanently on click
        var count = d[1] - d[0];
        svg.append("text")
          .attr("class", "count-label click-label")
          .attr("x", x(d.data.group) + x.bandwidth() / 2)
          .attr("y", y(d[1]) - 5)
          .attr("text-anchor", "middle")
          .text(count);
        });

        // Create a legend
        var legend = svg.append("g")
            .attr("class", "legend")
            .attr("transform", "translate(" + (width - 370) + ",10)");

        // Add legend squares
        legend.selectAll("legend")
            .data(subgroups)
            .enter()
            .append("rect")
            .attr("x", 0)
            .attr("y", function(d, i) { return i * 20; }) // Adjust the spacing as needed
            .attr("width", 10) // Adjust the square width
            .attr("height", 10) // Adjust the square height
            .style("fill", color);

        // Add legend labels
        legend.selectAll("text")
            .data(subgroups)
            .enter()
            .append("text")
            .attr("x", 20) // Position the label text
            .attr("y", function(d, i) { return i * 20 + 9; }) // Adjust the vertical position
            .style("font-size", "12px")
            .text(function(d) { return d; });


})


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
