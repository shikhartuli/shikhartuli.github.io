---
layout: page
permalink: /publications/
title: publications
description: 
years: [2023, 2022, 2021, 2020, 2019]
nav: true
---

It is easy to find most of my published work through my [Google Scholar page](https://scholar.google.com/citations?user=qiFEpzIAAAAJ&hl=en){:target="_blank"}.

<div class="publications">

{% for y in page.years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f papers -q @*[year={{y}}]* %}
{% endfor %}

</div>
