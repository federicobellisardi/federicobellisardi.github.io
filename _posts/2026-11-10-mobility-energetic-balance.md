---
title: "Do cities sit where moving around costs the least energy?"
description: >-
  A plain-language tour of our new preprint: across 56 cities, the real urban layout
  tends to need less movement energy than shifted, rotated or stretched versions of itself
  placed on the same terrain.
author: fbellisardi
date: 2026-11-10 10:00:00 +0100
categories: [Research, Preprint]
tags: [urban_mobility, topography, energy, cities, complex_systems]
math: true
pin: true
---

Anyone who has cycled up a hill knows that distance is only half of the story. A kilometre
uphill costs a lot more than a flat one. Cities are built on real terrain, with real hills,
valleys, rivers and coastlines. So we wondered whether the *shape* of a city reflects the energy
it takes to move through it.

That is the question behind our new preprint,
[**Mobility energetic balance frames spatial configuration of cities**](https://arxiv.org/abs/2610.21558),
written with Enrique Cano-Suñén, Ana Ruiz-Varona and José Javier Ramasco.

## The idea: move the city, keep everything else

You can't rebuild a city somewhere else to see what happens, but you can do it on a computer.
For each city we take three ingredients:

- the **road network**, from OpenStreetMap;
- the **terrain**, from a digital elevation model;
- the **travel demand**, meaning who goes where, estimated as origin–destination flows from geolocated social-media records.

We then pick the road network up and put it back down on the same landscape in a slightly
different position. We **shift** it by up to a few kilometres, **rotate** it by up to 40°, or
**stretch** it along one axis. The travel demand stays the same; only the layout's relationship
with the terrain changes. If the real city is "well placed", most of these alternatives should
cost more energy to move around in.

## A deliberately simple energy measure

We don't try to model every engine and every traffic light. For each trip along the network,
the energy has two parts:

$$
E_{\text{trip}} \;\approx\; \underbrace{\alpha \, L}_{\text{horizontal}} \;+\; \underbrace{m\,g\,\Delta h^{+}}_{\text{climbing}}
$$

where $L$ is the route length and $\Delta h^{+}$ is the total *uphill* elevation gained along the
way. Going downhill afterwards doesn't give the energy back. The constants correspond to a typical
private car. The point isn't the absolute number. It's a fair, comparable yardstick between the
real city and its displaced copies.

Routes are chosen by shortest path, not by lowest energy, so the result isn't baked into the
routing.

## What we found

We looked at **56 cities** in Europe, the Americas, Asia and Oceania, using functional urban
areas, which include the commuting zone and not just the historic core.

- In **26 cities** the real layout is the lowest-energy option among all the alternatives we tested.
- In **4 cities** a slightly displaced layout would be cheaper, and only by about 0.5–2.5%.
- The remaining cities are **constrained**: coastlines, lakes or the edges of the data rule out most displacements, so the comparison isn't meaningful.

The exceptions are the interesting part. In **Bogotá** the "cheaper" shift pushes the city west
onto the floodplain of the Bogotá River. In **Bandung** it moves toward volcanic highlands. In
**Buenos Aires** and **Brussels** it runs into a delta and into large railway and logistics
infrastructure. In other words, the terrain-energy argument still holds, but other constraints
win.

The climbing effort is also very unequal. Roughly **10% of street segments carry more than 60% of
all the uphill work**. A handful of steep, busy corridors take most of the cost of a city's
topography.

## Why it matters for planning

This doesn't prove that cities are "optimal", and it says nothing directly about how each city grew
historically. What it does show is a measurable, consistent link between **topography** and
**urban organisation**. That fits a picture where streets, mobility and terrain have adapted to each
other over time.

There's also a practical angle. In a test on **Barcelona** we placed 25,000 new residents at five
candidate sites with similar horizontal distances. The extra daily movement energy differed by
about **20%** between the best and the worst site, and almost all of the difference came from
climbing. When cities plan growth or densification, terrain-related movement costs are worth putting
on the table next to distance.

## Limitations

Social-media data over-represent some groups. The energy model is car-based. African cities are
missing for lack of data. The results depend on how the urban area is defined, and administrative
boundaries give a noticeably different picture than functional urban areas. All of this is
discussed in the paper.

📄 **Read the preprint:** [arXiv:2610.21558](https://arxiv.org/abs/2610.21558)
