---
layout: page
title: Reach-Avoid Games
description: Efficient multi-agent reach-avoid dynamic games solver
img: assets/img/reach-avoid-games-demo-rotated.gif
importance: 6
category: work
related_publications: true
---

This project {% cite reach-avoid-games %} implements and demonstrates computationally efficient, **time-consistent solutions to multi-agent reach-avoid dynamic games**, a class of safety-critical optimal control problems where agents aim to **reach goal sets while avoiding failure conditions** under adversarial or interactive dynamics. These games are widely used as formal models in mobile robot motion planning, autonomous driving, and safety-critical decision making.

Our implementation supports single and multi-player reach-avoid environments, including cooperative and adversarial interactions, with tools for training, evaluation, and visualization.

## Core Idea
A reach-avoid game involves agents that must:
- **Reach a specified target** 
- **Avoid unsafe regions or adversarial opponents**

Reach-avoid cost is formulated, such that past failures override future successes. The reach-avoid condition for a generic state trajectory $\mathbb{x} = (x_0, \dots, x_T)$ can be expressed as:

$$
\exists t \in \{0,\dots,T\} : x_t \in \mathcal{T}_t \wedge \forall \tau \in \{0,\dots,t\} : x_\tau \not\in \mathcal{F}_\tau
$$

Solutions are **time-consistent**, meaning that planned trajectories remain optimal at all timesteps (later control inputs are still optimal despite
suboptimal behavior earlier in the trajectory), or **time-inconsistent** (pinch-point solution).

## Highlights & Demos
### Single-Player Reach-Avoid
One agent navigates a free space with obstacles toward a goal while maintaining safety constraints. We show the result from both time-inconsistent (pinch-point) and time-consistent solution:

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid
        loading="eager"
        path="assets/img/rag-time-inconsistent-training.gif"
        title="RAG time-inconsistent single-agent training"
        class="img-fluid rounded z-depth-1" 
        style="height: 400px; object-fit: cover;"
        %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid
        loading="eager"
        path="assets/img/rag-time-consistent-training.gif"
        title="RAG time-consistent single-agent training"
        class="img-fluid rounded z-depth-1" 
        style="height: 400px; object-fit: cover;"
        %}
    </div>
</div>
<div class="caption">
  <b>Figure:</b> Time-inconsistent (left) and time-consistent (right) solution for reach-avoid games of single-agent.
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid
        loading="eager"
        path="assets/img/exp_time_inconsistent_summary_three_color_plot.png"
        title="RAG time-inconsistent single-agent training, batch"
        class="img-fluid rounded z-depth-1" 
        style="height: 400px; object-fit: cover;"
        %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid
        loading="eager"
        path="assets/img/exp_time_consistent_summary_three_color_plot.png"
        title="RAG time-consistent single-agent training, batch"
        class="img-fluid rounded z-depth-1" 
        style="height: 400px; object-fit: cover;"
        %}
    </div>
</div>
<div class="caption">
  <b>Figure:</b> Batch run of time-inconsistent (left) and time-consistent (right) solution for reach-avoid games of single-agent.
</div>

### Multi-Player Scenarios
- **Two-Player Interactions**: Cooperative or adversarial reach-avoid dynamics  
- **Three-Player Games**: Complex interaction patterns demonstrating scalable behavior synthesis

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid
        loading="eager"
        path="assets/img/rag-adversarial-rollout.gif"
        title="RAG 2-player adversarial case"
        class="img-fluid rounded z-depth-1" 
        style="height: 400px; object-fit: cover;"
        %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid
        loading="eager"
        path="assets/img/rag-three-players-training-rollout.gif"
        title="RAG 3-player case"
        class="img-fluid rounded z-depth-1" 
        style="height: 400px; object-fit: cover;"
        %}
    </div>
</div>
<div class="caption">
  <b>Figure:</b> Reach-avoid games solution for two-player adversarial scenario (left) and three-player scenario (right).
</div>

## Publication
This work was accepted to ICRA 2022 as [Back to the Future: Efficient, Time-Consistent Solutions in Reach-Avoid Games](https://arxiv.org/abs/2109.07673), introducing algorithms for efficiently computing solutions that remain optimal under execution perturbations.