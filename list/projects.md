---
title: All Projects
narrow: true
permalink: list/projects.html
show_profile: true
---

{% assign sorted = site.projects | reverse %}

{% for project in sorted %}
  {% include components/project-card.html %}
{% endfor %}
