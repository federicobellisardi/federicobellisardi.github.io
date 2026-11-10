---
layout: page
title: About
icon: fas fa-info-circle
order: 0
toc: false
permalink: /
---

<div class="profile-hero">
  <picture>
    <source srcset="{{ '/assets/img/winter.webp' | relative_url }}" type="image/webp" />
    <img
      class="profile-hero__photo"
      src="{{ '/assets/img/winter.png' | relative_url }}"
      alt="Portrait of Federico Bellisardi"
      width="400"
      height="400"
      fetchpriority="high"
    />
  </picture>

  <div class="profile-hero__body">
    <h2 class="profile-hero__name">Federico Bellisardi</h2>

    <p class="profile-hero__role">
      Postdoctoral Researcher at
      <a href="https://ifisc.uib-csic.es/" target="_blank" rel="noopener noreferrer">IFISC (UIB&ndash;CSIC)</a>,
      Palma de Mallorca
    </p>

    <p class="profile-hero__summary">
      I build data-driven and physics-informed models of complex systems, with a
      focus on urban mobility: how people move through a city, why it congests,
      and what can be done about it.
    </p>

    <ul class="link-pills">
      {%- for profile in site.data.profiles -%}
        {%- if profile.home -%}
          <li>
            <a
              href="{{ profile.url }}"
              {% unless profile.url contains 'mailto:' %}target="_blank" rel="noopener noreferrer"{% endunless %}
            >
              <i class="{{ profile.icon }}" aria-hidden="true"></i>{{ profile.name }}
            </a>
          </li>
        {%- endif -%}
      {%- endfor -%}
      <li>
        <a href="{{ site.cv_path | relative_url }}" target="_blank" rel="noopener noreferrer">
          <i class="fas fa-file-pdf" aria-hidden="true"></i>Curriculum Vitae
        </a>
      </li>
    </ul>
  </div>
</div>

---

## Biography

I am a physicist working on **urban mobility** with the tools of **complex
systems** and **data science**. I want to understand how people and vehicles move
through cities, why networks congest, and how the shape of a city and the terrain
it sits on affect the cost of getting around.

I did my PhD in **Physics** at the **University of Bologna**, supervised by
Armando Bazzani, and defended it in May 2025. My thesis,
[*Data analytics and predictive models for sustainable multimodal mobility in future smart cities*](https://doi.org/10.48676/unibo/amsdottorato/12316),
combined Wi-Fi, mobile-phone and road-sensor data with agent-based and
optimal-velocity models.

I am now a postdoctoral researcher at **IFISC**, the Institute for
Cross-Disciplinary Physics and Complex Systems in Palma de Mallorca. Recently I
have been studying how topography and the energy cost of moving shape the spatial
organisation of cities, comparing [56 cities worldwide](https://arxiv.org/abs/2610.21558).

I like models that are simple enough to understand and grounded enough in real
data to be useful for planning. I am also interested in how physics and machine
learning can work together, for example in physics-informed neural networks.

## Research interests

<div class="card-grid">
  <div class="card-grid__item">
    <h3><i class="fas fa-mountain-city" aria-hidden="true"></i> Cities, terrain and energy</h3>
    <p>How topography and movement energy relate to the spatial configuration of cities.</p>
  </div>
  <div class="card-grid__item">
    <h3><i class="fas fa-project-diagram" aria-hidden="true"></i> Congestion on networks</h3>
    <p>Random walks, maximum entropy and the transition to congestion on road graphs.</p>
  </div>
  <div class="card-grid__item">
    <h3><i class="fas fa-users" aria-hidden="true"></i> Agent-based &amp; traffic simulation</h3>
    <p>Pedestrian and vehicular models, from heritage city centres to regional road networks.</p>
  </div>
  <div class="card-grid__item">
    <h3><i class="fas fa-satellite-dish" aria-hidden="true"></i> Mobility data analytics</h3>
    <p>Turning Wi-Fi, mobile-phone, sensor and geolocated data into origin&ndash;destination flows and forecasts.</p>
  </div>
</div>

## Selected publications

{% include publication-list.html max=3 %}

[See all publications &rarr;]({{ '/publications/' | relative_url }})

## Latest notes

<ul class="post-teasers">
{%- for post in site.posts limit: 3 -%}
  <li>
    <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: '%b %-d, %Y' }}</time>
    <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
  </li>
{%- endfor -%}
</ul>

[Browse the blog &rarr;]({{ '/blog/' | relative_url }})
