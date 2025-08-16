---
layout: default
title: Publications
permalink: /publications/
---

# Publications

Below are selected publications from my research. They are listed in reverse chronological order.

{% assign pubs = site.data.publications.papers | sort: "year" | reverse %}
{% for pub in pubs %}
**{{ pub.authors }}** ({{ pub.year }}). *{{ pub.title }}*. {{ pub.venue }}{% if pub.details %}. {{ pub.details }}{% endif %}  
{% endfor %}
