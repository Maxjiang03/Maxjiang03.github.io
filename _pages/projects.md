---
layout: archive
title: "Projects"
permalink: /projects/
author_profile: true
---

{% include base_path %}

{% comment %} Order follows the numeric filename prefix in _portfolio/ {% endcomment %}
{% for post in site.portfolio %}
  {% include archive-single.html %}
{% endfor %}
