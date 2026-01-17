---
layout: page
title: Driveway
description: Data-driven simulator for closed-loop RLFT
img: assets/img/womd-on-waymax-crop.gif
importance: 4
category: work
related_publications: true
---

Driveway (Meta**Drive** + **Way**max) is a data generation and training pipeline designed to enable closed-loop reinforcement learning fine-tuning (RLFT) for autonomous driving at scale, connecting existing scenario generation frameworks with a JAX-native simulator

Driveway is an integration layer that combines:
* MetaDrive / ScenarioNet for scenario generation and dataset diversity
* Waymax for efficient, JAX-compatible closed-loop simulation

The goal is to make procedurally generated and multi-dataset scenarios usable inside a simulator that is already well-aligned with modern ML training pipelines.

---
## Motivation
Closed-loop RLFT for autonomous driving places two practical requirements on a simulator:

**1. ML-infrastructure compatibility**
The simulator must integrate cleanly with large-scale, accelerator-backed training pipelines.
→ Waymax is chosen because it is JAX-native, enabling vectorized rollouts, differentiation, and tight coupling with model training.

**2. Scenario diversity and data flexibility**
RLFT requires exposure to both in-distribution and systematically generated out-of-distribution scenarios.
→ MetaDrive, together with ScenarioNet, provides mature tooling for:

* Procedural scenario generation
* Support for multiple datasets and benchmarks
* Controlled variation over map layouts and traffic configurations

No single existing platform satisfied both requirements simultaneously.

---
## Core Idea

Driveway connects MetaDrive-style scenario generation to Waymax-style closed-loop simulation through a structured data pipeline.

* MetaDrive / ScenarioNet act as scenario backends
* Waymax acts as the simulation frontend
* Driveway translates scenarios between the two without modifying either system’s core design

This allows scenarios that are:
* Generated procedurally
* Loaded from diverse datasets
* Parameterized for stress testing

to be executed inside a JAX-friendly closed-loop simulator suitable for RLFT.

---
## System Flow

**1. Scenario Generation**
* MetaDrive / ScenarioNet generate or load scenarios
* Supports both logged datasets and procedurally generated variants

**2. Data Translation**
* Scenarios are converted into a Waymax-compatible representation
* Preserves road geometry, agent states, and temporal structure

**3. Closed-Loop Execution**
* Waymax executes the scenario in closed loop
* Ego policies interact with reactive agents via IDM

**4. Training Integration**
* Rollouts are consumed directly by RLFT pipelines
* Compatible with large-scale JAX training workflows

---
## Result
Roadgraph feature types between MetaDrive and Waymax are consolidated, so that scenarios from MetaDrive and easily be loaded and used in Waymax:

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid
      loading="eager"
      path="assets/img/metadrive-to-waymax-roadgraph.png"
      title="MetaDrive to Waymax roadgraph mapping"
      class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  <b>Figure:</b> Roadgraph mapping between MetaDrive scene representation and Waymax scene representation.
</div>

The following figures show a scenario created with MetaDrive, loaded in Waymax, and controlled using Waymax's IDM.

<div class="row justify-content-sm-center">
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid
      path="assets/img/metadrive_to_waymax_replay.gif"
      title="WOMD to MetaDrive to Waymax replay"
      class="img-fluid rounded z-depth-1" 
      style="height: 250px; object-fit: scale-down;"
    %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid
      path="assets/img/metadrive_waymax_generated_replay.gif"
      title="Generated MetaDrive scene to Waymax replay"
      class="img-fluid rounded z-depth-1" 
      style="height: 250px; object-fit: scale-down;"
    %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid
      path="assets/img/waymax_simulator_demo.gif"
      title="Generated MetaDrive scene to Waymax, controlled via IDM"
      class="img-fluid rounded z-depth-1"
      style="height: 250px; object-fit: scale-down;"
    %}
  </div>
</div>
<div class="caption">
  <b>Figure:</b> Driveway in action. From left to right: a scenario generated in MetaDrive and replayed in Waymax; a procedurally generated MetaDrive scene loaded into Waymax; and the same scene executed in closed loop with surrounding traffic controlled by Waymax’s Intelligent Driver Model (IDM).
</div>

Using Driveway, we can create and inverleave numerous scenarios, both in-distribution and out-of-distribution. In addition, when combined with previous works in game-theoretic multi-agent trajectory optimization in adversarial context {% cite reach-avoid-games %}, we can create true adversarial scenarios on top.