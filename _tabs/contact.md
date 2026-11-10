---
layout: page
title: Contacts
icon: fas fa-address-book
permalink: /contact/
order: 6
toc: false
---

The fastest way to reach me is email — I read it daily and usually reply within a
couple of working days.

## Email

<ul class="link-pills">
  <li>
    <a href="mailto:fbellisardi@ifisc.uib-csic.es">
      <i class="fas fa-envelope" aria-hidden="true"></i>fbellisardi@ifisc.uib-csic.es
    </a>
  </li>
  <li>
    <a href="mailto:bellisardi@gmail.com">
      <i class="fas fa-envelope" aria-hidden="true"></i>bellisardi@gmail.com
    </a>
  </li>
</ul>

## Academic profiles

<ul class="link-pills">
  {%- for profile in site.data.profiles -%}
    {%- if profile.group == 'academic' -%}
      {%- unless profile.url contains 'mailto:' -%}
        <li>
          <a href="{{ profile.url }}" target="_blank" rel="noopener noreferrer">
            <i class="{{ profile.icon }}" aria-hidden="true"></i>{{ profile.name }}
          </a>
        </li>
      {%- endunless -%}
    {%- endif -%}
  {%- endfor -%}
</ul>

## Code and social

<ul class="link-pills">
  {%- for profile in site.data.profiles -%}
    {%- if profile.group == 'code' or profile.group == 'social' -%}
      <li>
        <a href="{{ profile.url }}" target="_blank" rel="noopener noreferrer">
          <i class="{{ profile.icon }}" aria-hidden="true"></i>{{ profile.name }}
        </a>
      </li>
    {%- endif -%}
  {%- endfor -%}
</ul>

## Where to find me

<address>
  <strong>IFISC</strong> — Institute for Cross-Disciplinary Physics and Complex Systems<br />
  Campus Universitat de les Illes Balears, Carretera de Valldemossa km 7.5<br />
  Edificio Científico-Técnico, 07122 Palma de Mallorca<br />
  Balearic Islands, Spain
</address>

<div id="ifisc-map" role="region" aria-label="Map showing IFISC in Palma de Mallorca"></div>

<link
  rel="stylesheet"
  href="https://cdn.jsdelivr.net/npm/leaflet@1.9.4/dist/leaflet.css"
  integrity="sha256-p4NxAoJBhIIN+hmNHrzRCf9tD/miZyoHS5obTRR9BMY="
  crossorigin="anonymous"
/>
<script
  defer
  src="https://cdn.jsdelivr.net/npm/leaflet@1.9.4/dist/leaflet.js"
  integrity="sha256-20nQCchB9co0qIjJZRGuk2/Z9VM+kNiyxNV1lvTlZBo="
  crossorigin="anonymous"
></script>
<script>
  (function () {
    var COORDS = [39.63667, 2.648797];

    function initMap() {
      var container = document.getElementById('ifisc-map');
      if (!container || typeof L === 'undefined') {
        return;
      }

      var map = L.map(container, { scrollWheelZoom: false }).setView(COORDS, 14);

      L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        maxZoom: 19,
        attribution:
          '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
      }).addTo(map);

      L.marker(COORDS)
        .addTo(map)
        .bindPopup('IFISC (UIB&ndash;CSIC), Palma de Mallorca')
        .openPopup();
    }

    /* `defer` guarantees Leaflet is parsed before DOMContentLoaded fires, but
       the event may already have fired when the page comes back from the
       bfcache. NOTE: `compress_html` collapses newlines in production, so this
       script must not use `//` comments. */
    if (document.readyState === 'loading') {
      document.addEventListener('DOMContentLoaded', initMap);
    } else {
      initMap();
    }
  })();
</script>
