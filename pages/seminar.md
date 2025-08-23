---
layout: default
title: Seminar
permalink: /seminar/
---

{% assign sections = site.data.data.projects %}

{%- comment -%}
1) "Seminar Work"를 정확히 찾되,
2) 못 찾으면 title에 'seminar'가 포함된 섹션을 대소문자 무시하고 검색
{%- endcomment -%}
{% assign seminar = sections | where: "title", "Seminar Work" | first %}
{% if seminar == nil %}
  {% assign seminar = sections | where_exp: "s", "s.title and s.title downcase contains 'seminar'" | first %}
{% endif %}

<section class="section seminar-section">
  <h2 class="section-title">
    <span class="fa-stack fa-xs">
      <i class="fas fa-circle fa-stack-2x"></i>
      <i class="fas fa-chalkboard-teacher fa-stack-1x fa-inverse"></i>
    </span>
    Seminar
  </h2>

  {% if seminar %}
    {% if seminar.intro %}
      <div class="intro"><p>{{ seminar.intro }}</p></div>
    {% endif %}

    {% for work in seminar.assignments %}
      {%- assign anchor = work.title | slugify -%}
      <div class="item" id="{{ anchor }}">
        <div class="meta">
          <div class="upper-row">
            <h3 class="job-title">
              {% if work.link %}
                <a href="{{ work.link }}" target="_blank">{{ work.title }}</a>
              {% else %}
                {{ work.title }}
              {% endif %}
            </h3>
            {% if work.time %}<div class="time">{{ work.time }}</div>{% endif %}
          </div>
          {% if work.affiliation %}<div class="company">{{ work.affiliation }}</div>{% endif %}
        </div>

        {% if work.tagline %}
          <div class="details">{{ work.tagline }}</div>
        {% endif %}

        {%- comment -%}
        파일 임베드: work.files (배열) 우선, 없으면 work.file(단일) 지원
        {%- endcomment -%}
        {% assign file_list = nil %}
        {% if work.files %}
          {% assign file_list = work.files %}
        {% elsif work.file %}
          {% assign file_list = work.file | split: '||' %}
        {% endif %}

        {% if file_list %}
          {% for f in file_list %}
            {% assign f_lower = f | downcase %}
            {% if f_lower contains '.pdf' %}
              <div class="embed-wrap">
                <object data="{{ f | relative_url }}" type="application/pdf" width="100%" height="640">
                  <iframe src="{{ f | relative_url }}" width="100%" height="640"></iframe>
                </object>
                <p class="download-hint"><a href="{{ f | relative_url }}" download>Download PDF</a></p>
              </div>
            {% elsif f_lower contains '.ppt' %}
              <div class="embed-wrap">
                <iframe
                  src="https://view.officeapps.live.com/op/embed.aspx?src={{ site.url | append: f | uri_escape }}"
                  width="100%" height="640" frameborder="0">
                </iframe>
                <p class="download-hint"><a href="{{ f | relative_url }}" download>Download PPT</a></p>
              </div>
            {% endif %}
          {% endfor %}
        {% endif %}
      </div>
    {% endfor %}
  {% else %}
    <p>No seminar items found. Check <code>_data/data.yml</code> → <code>projects:</code>에 “Seminar Work” 섹션이 있는지 확인해 주세요.</p>
  {% endif %}
</section>
