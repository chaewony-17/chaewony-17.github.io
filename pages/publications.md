---
layout: default
title: Publications
permalink: /publications/
---

# {{ site.data.data.publications.title | default: "Publications" }}

{%- comment -%}
우선순위대로 데이터 소스 탐색:
- site.data.data.publications (당신이 넣은 위치)
- site.data.publications
- site.data.resume.publications
{%- endcomment -%}
{% assign pubs_src = site.data.data.publications | default: site.data.publications | default: site.data.resume.publications %}

{% if pubs_src and pubs_src.papers %}
  {% assign pubs = pubs_src.papers | sort: "year" | reverse %}
  {% for pub in pubs %}
- **{{ pub.authors }}** ({{ pub.year }}). *{{ pub.title }}*. {{ pub.conference }}
  {% endfor %}
{% else %}
_ No publications found. Please check `_data/data.yml` → `publications:` or add `_data/publications.yml`. _
{% endif %}
