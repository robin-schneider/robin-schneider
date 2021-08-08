---
layout: page
permalink: /publications/
title: publications
description: > 
  Here is a list of all my publications. 
years: [2021, 2020, 2019, 2017]
nav: true
---

You can also find me on <a href="https://inspirehep.net/authors/1635417?ui-citation-summary=true" target="_blank">iNSPIRE</a> and <a href="https://scholar.google.com/citations?user=3b2YBTcAAAAJ&hl=en" target="_blank">Google scholar</a>.

<div class="publications">

{% for y in page.years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f papers -q @*[year={{y}}]* %}
{% endfor %}

</div>
