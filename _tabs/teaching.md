---
layout: page
title: Teaching
icon: fas fa-graduation-cap
permalink: /teaching/
order: 3
toc: false
---

## Thesis co-supervision

<ul class="pub-list">
  {%- for t in site.data.supervision -%}
    <li>
      <span class="pub-list__title">
        {%- if t.url -%}
          <a href="{{ t.url }}" target="_blank" rel="noopener noreferrer">{{ t.title }}</a>
        {%- else -%}
          {{ t.title }}
        {%- endif -%}
      </span>
      <span class="pub-list__authors">{{ t.student }} &middot; {{ t.level }}</span>
      <span class="pub-list__venue">
        {{- t.programme }}, {{ t.year }}{% if t.cosupervisors %} &middot; co-supervised with {{ t.cosupervisors }}{% endif -%}
      </span>
    </li>
  {%- endfor -%}
</ul>

## Teaching

<ul class="pub-list">
  {%- for c in site.data.teaching -%}
    <li>
      <span class="pub-list__title">{{ c.course }}</span>
      <span class="pub-list__venue">{{ c.programme }}, {{ c.years }}</span>
    </li>
  {%- endfor -%}
</ul>
