---
layout: archive
title: "Projects"
permalink: /projects/
author_profile: true
---

<style>
body {
text-align: justify}
</style>

You can also find my articles on [Google scholar profile](https://scholar.google.com/citations?user=D7z8d5sAAAAJ&hl=en).

{% include base_path %}

{% for post in site.projects reversed %}
  {% include archive-single.html %}
{% endfor %}
