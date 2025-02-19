---
layout: post
title: Contacts
icon: fas fa-address-book
permalink: /contact/
order: 5
---

<div align="center">
  <h2><strong>📬 GET IN TOUCH</strong></h2>
</div>


### 📧 Email  
[<i class="fa fa-envelope" aria-hidden="true"></i> fbellisardi@ifisc.uib-csic.es](mailto:fbellisardi@ifisc.uib-csic.es)  | [<i class="fa fa-envelope" aria-hidden="true"></i> bellisardi@gmail.com](mailto:bellisardi@gmail.com)  

### 💼 Professional Profiles  
[<i class="fab fa-github"></i> GitHub](https://github.com/federicobellisardi) | [<i class="fab fa-linkedin"></i> LinkedIn](https://www.linkedin.com/in/federico-bellisardi-459b40165) | [<i class="fa-brands fa-google-scholar"></i> Google Scholar](https://scholar.google.com/citations?user=Ba8WR_8AAAAJ&hl) | [<i class="fa-brands fa-researchgate"></i> ResearchGate](https://www.researchgate.net/profile/Federico-Bellisardi-3)  

### 🌍 Social & Messaging  
[<i class="fa-brands fa-x-twitter"></i> Twitter/X](https://x.com/FBellisardi) | [<i class="fa-brands fa-telegram"></i> Telegram](https://t.me/federicobellisardi) | [<i class="fa-brands fa-whatsapp"></i> WhatsApp](https://wa.me/622632102)  

### 🔗 Website  
[<i class="fa-solid fa-globe"></i> Personal Website](https://federicobellisardi.github.io)  

---

<div align="center">
  <h2><strong>📍 LOCATION</strong></h2>
</div>

[IFISC](https://ifisc.uib-csic.es/en/) - Institute for Cross-Disciplinary Physics and Complex Systems  
Campus Universitat de les Illes Balears Carretera de Valldemossa, km 7,5 Edificio Científico-Técnico, 07122 Palma de Mallorca,Islas Baleares, Balearic Islands 

<head>
  <link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />
  <script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>
</head>
<body>

  <div id="map" style="height: 400px; width: 100%;"></div>

  <script>
    function initMap() {
      var map = L.map('map').setView([39.636670, 2.648797], 10);

      L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '© OpenStreetMap contributors'
      }).addTo(map);

      L.marker([39.636670, 2.648797]).addTo(map)
        .bindPopup('IFISC, Palma de Mallorca')
        .openPopup();
    }

    document.addEventListener("DOMContentLoaded", initMap);
  </script>

</body>
<link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />
