---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

For now, please refer to my university page here: https://www.cl.uzh.ch/de/people/team/compling/mmueller.html

{% if author.googlescholar %}
  You can also find my articles on <u><a href="{{author.googlescholar}}">my Google Scholar profile</a>.</u>
{% endif %}

{% include base_path %}

{% for post in site.publications reversed %}
  {% include archive-single.html %}
{% endfor %}
