---
layout: default
title: Seminar
permalink: /seminar/
---

{% assign sections = site.data.data.projects %}
{% assign seminar = sections | where: "title", "Seminar Work" | first %}

{% if seminar %}
<section class="section seminar-section">
  <h2 class="section-title">
    <span class="fa-stack fa-xs">
      <i class="fas fa-circle fa-stack-2x"></i>
      <i class="fas fa-chalkboard-teacher fa-stack-1x fa-inverse"></i>
    </span>
    {{ seminar.title }}
  </h2>

  {% if seminar.intro %}
    <div class="intro"><p>{{ seminar.intro }}</p></div>
  {% endif %}

  {% for work in seminar.assignments %}
    {%- assign anchor = work.title | slugify -%}
    <div class="item" id="{{ anchor }}">
      <div class="project-title">
        {% if work.link %}
          <a href="{{ work.link }}" target="_blank">{{ work.title }}</a>
        {% else %}
          {{ work.title }}
        {% endif %}
      </div>
      {% if work.tagline %}
        <div class="details">{{ work.tagline }}</div>
      {% endif %}

      {% if work.file %}
        {%- assign lower = work.file | downcase -%}
        {%- if lower contains '.pdf' -%}
          <!-- PDF 임베드 -->
          <div class="embed-wrap">
            <object data="{{ work.file | relative_url }}" type="application/pdf" width="100%" height="600">
              <iframe src="{{ work.file | relative_url }}" width="100%" height="600"></iframe>
            </object>
            <p class="download-hint">
              <a href="{{ work.file | relative_url }}" download>Download PDF</a>
            </p>
          </div>
        {%- elsif lower contains '.ppt' -%}
          <!-- PPT/PPTX 임베드 (Office Web Viewer) -->
          <div class="embed-wrap">
            <iframe
              src="https://view.officeapps.live.com/op/embed.aspx?src={{ site.url | append: work.file | uri_escape }}"
              width="100%" height="600" frameborder="0">
            </iframe>
            <p class="download-hint">
              <a href="{{ work.file | relative_url }}" download>Download PPT</a>
            </p>
          </div>
        {%- endif -%}
      {% endif %}
    </div>
  {% endfor %}
</section>
{% endif %}
