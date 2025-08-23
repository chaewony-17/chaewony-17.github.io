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
    <div class="item">
      <span class="project-title">
        {% if work.link %}
          <a href="{{ work.link }}" target="_blank">{{ work.title }}</a>
        {% else %}
          {{ work.title }}
        {% endif %}
      </span>
      {% if work.tagline %}
        <div class="details">{{ work.tagline }}</div>
      {% endif %}
    </div>
  {% endfor %}
</section>
{% endif %}
