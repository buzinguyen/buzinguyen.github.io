---
layout: single
title: "Back to the Future: Efficient, Time-Consistent Solutions in Reach-Avoid Games"
categories: Research
permalink: research/reach-avoid-games
tags: 
    - Robotics 
    - Game Theory
excerpt: >
    An extension of the state-of-the-art multi-agent non-cooperative Nash trajectory optimization solver (iLQSolver) that deals with time-consistency in solution.
header:
    overlay_image: 
    overlay_filter: 0.5
    actions:
    - label: "Paper"
      url: https://arxiv.org/pdf/2109.07673.pdf
---

We study the class of reach-avoid dynamic games in which multiple agents interact noncooperatively, and each wishes to satisfy a distinct target criterion while avoiding a failure criterion. Reach-avoid games are commonly used to express safety-critical optimal control problems found in mobile robot motion planning. Here, we focus on finding time-consistent solutions, in which future motion plans remain optimal even when a robot diverges from the plan early on due to, e.g., intrinsic dynamic uncertainty or extrinsic environment disturbances. Our main contribution is a computationally-efficient algorithm for multi-agent reach-avoid games which renders time-consistent solutions for all players. We demonstrate our approach in two- and three-player simulated driving scenarios, in which our method provides safe control strategies for all agents.

<figure>
    <p float="left" style="text-align:center;">
        <img src="https://github.com/SafeRoboticsLab/Reach-Avoid-Games/raw/main/result/experiment_2022-02-28-11_42_44/figures/evaluate_training.gif" width="300">
        <img src="https://github.com/SafeRoboticsLab/Reach-Avoid-Games/raw/main/result/experiment_2022-02-28-11_46_04/figures/evaluate_training.gif" width="300">
    </p>
    <figcaption align="center"><b>Figure 1: One-player time-consistent (left) and pinch-point (right)</b></figcaption>
<figure>

<figure>
    <p float="left" style="text-align:center;">
        <img src="https://github.com/SafeRoboticsLab/Reach-Avoid-Games/raw/main/result/experiment_2022-02-21-20_51_25/evaluate/evaluate_rollout.gif" width="400">
    </p>
    <figcaption align="center"><b>Figure 2: Three-player solution</b></figcaption>
</figure>