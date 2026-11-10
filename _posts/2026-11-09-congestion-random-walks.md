---
title: "How traffic jams are born on a graph"
description: >-
  A short introduction to our Entropy paper on congestion in a minimal transport model:
  random walks on a network with finite capacity, maximum entropy, and the role of fluctuations
  as an early warning of congestion.
author: fbellisardi
date: 2026-11-09 10:00:00 +0100
categories: [Research, Paper]
tags: [congestion, random_walks, networks, statistical_physics, traffic]
pin: false
---

Congestion is one of the most familiar problems in a city, and one of the hardest to predict. Real
traffic depends on drivers, signals, accidents and the weather. In our paper
[**Congestion Transition on Random Walks on Graphs**](https://doi.org/10.3390/e26080632)
(*Entropy*, 2024), written with Luca Di Meco, Mirko Degli Esposti and Armando Bazzani, we took the
opposite approach. We stripped the problem down to the minimum and asked what congestion looks like
when almost nothing is left.

## A minimal model

Think of the road network as a **graph**:

- every **node** is a location. It can hold a maximum number of vehicles (its *capacity*) and can let them out only at a maximum rate (its *maximum flow*);
- every **link** has a weight that sets how likely a vehicle is to move from one node to the next. Taken together, the weights encode the mobility demand.

Vehicles move as **random walkers** on this graph. We look at stationary states, where on average
as many vehicles enter each node as leave it.

## A percolation-like transition

In the simplest version of the dynamics, where nodes update one at a time, the problem can be solved
analytically with a **local maximum-entropy principle**. As the total number of vehicles grows,
congested nodes start to appear, and each congested node appears as an *independent random event*.
This is very similar to a **percolation transition**.

## Synchronous dynamics: entropic forces

The more realistic case is the one where all nodes update **at the same time**, and there the picture
changes. Numerical simulations show that **entropic forces** create correlations between the states of
neighbouring nodes. Empty nodes tend to cluster with other empty nodes, and congested nodes with other
congested nodes. Congestion stops being a scatter of isolated points and becomes collective.

## Why fluctuations matter

The broader goal is to find the **universal** features of how congestion forms, meaning the ones that
don't depend on the details of a specific city. The most interesting candidate is the role of
**fluctuations in the traffic load**. They can act as a *precursor*, an early sign that a transport
network is getting close to congestion.

📄 **Read the paper (open access):** [doi:10.3390/e26080632](https://doi.org/10.3390/e26080632)
