---
title: Ocean eddy detection
description: Segmenting ocean eddies from sea surface temperature, sea level and current maps, for Mercator Ocean's challenge.
summary: "Three days, five people: a U-Net and a gradient-boosting model to find cyclonic and anticyclonic eddies in ocean maps."
year: 2023
context: Mercator Ocean challenge
group: ml
order: 2
tools: [Python, PyTorch, U-Net, LightGBM, xarray]
facts:
  - label: Team
    value: 5 people, 3 days
links:
  - label: Challenge on Kaggle
    url: https://www.kaggle.com/competitions/ocean-eddy-detection/overview
card: /assets/img/ocean/card.jpg
image: /assets/img/ocean/card.jpg
cover: /assets/img/ocean/cover.jpg
cover_alt: Turbulent ocean water seen from above
redirect_from:
  - /2023-02-27-ocean/
---

## Context

[Mercator Ocean](https://www.kaggle.com/competitions/ocean-eddy-detection/overview) set this challenge to narrow the gap between simulated oceans and the real one. Detecting eddies with AI makes it possible to check ocean models against reality. That matters for operational oceanography and for uses such as simulating how floating objects drift.

The goal was a deep learning model that finds eddies using three inputs: sea surface temperature (SST), sea level anomalies (SLA) and ocean current maps. Methods based on SLA alone have known limits. The dataset contained gridded "images" of these variables, labeled with the outlines of the eddies to find.

<figure>
  <img class="diagram" src="{{ '/assets/img/ocean/eddy-physics.png' | relative_url }}" alt="Diagram of a cyclonic and an anticyclonic eddy, showing how each one shifts sea level and water temperature" width="850" height="708" loading="lazy">
  <figcaption>How eddies show up in sea level and temperature.</figcaption>
</figure>

## Approach

The first job was **cleaning the data**: outliers, very high variance and missing values. The model also had to predict no eddies on land, where there was no data at all.

To get early results, we started on a **sub-region far from the coast** that needed little preprocessing. Those first results then shaped the rest of the work.

We handled the data with **xarray** and split into two sub-teams:

- **Deep learning:** a U-Net trained from scratch in PyTorch.
- **Classic machine learning:** gradient boosting with LightGBM, adding spatial context by hand through engineered gradient features.

## Results

The U-Net worked best, perhaps partly because it was quicker to get running in the time we had. It reached an accuracy of about **0.7** across the three classes: cyclonic eddy, anticyclonic eddy and no eddy.

<figure>
  <img class="diagram" src="{{ '/assets/img/ocean/results.png' | relative_url }}" alt="Two maps side by side: labeled eddies on the left, the model's predicted eddies on the right" width="1400" height="418" loading="lazy">
  <figcaption>Ground truth (left) and U-Net predictions (right) on the full map.</figcaption>
</figure>
