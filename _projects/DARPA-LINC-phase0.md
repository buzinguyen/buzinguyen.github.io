---
layout: page
title: DARPA LINC Phase 0
description: Learning Introspective Control for safety-critical field robots
img: assets/img/wedge-terrain-preview.gif
importance: 1
category: work
related_publications: true
selected: true
---
<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid
      loading="eager"
      path="assets/img/darpa-linc.png"
      title="DARPA LINC GVR robot on wedge terrain"
      class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  <b>Figure:</b> Safety Enforcer interface illustrating how operator commands are filtered through learned safety constraints before execution.
</div>

## Overview

In **DARPA Learning Introspective Control (LINC) Phase 0**, we explore how learning-based *Safety Enforcers* can enable shared autonomy for safety-critical field robots, by intervening only when necessary, while preserving operator intent and avoiding disruptive or surprising behaviors.

Specifically, we developed and deployed a learning-based safety filter for a hybrid tracked robot operating across challenging terrains (wedge, single-track incline, narrowing corridor, and chicane), culminating in a fully integrated **final field test** under unmodeled disturbances.

A central design objective of the program is robustness under **adversarial and degraded conditions**. During deployment, adversarial disturbances may corrupt or disable visual sensing and induce actuator-level degradation. As a result, all Safety Enforcers are trained without camera observations, and must remain effective under partial actuaion loss or altered actuator dynamics. **<u>The resulting safety policy relies exclusively on proprioceptive state</u>** (e.g., IMU, joint states, velocities), ensuring safe operation even when vision is unavailable and actuation is imperfect.

**Key contributions:**
- Minimal task disruption: maintained safety while preserving operator intent.
- Not only did not impede progress, but improved challenging terrain traversal.
- Novice-driver friendly: operator can focus on the task, safety is automatic.

---

## System Overview: Learning Introspective Control

The Safety Enforcer continuously monitors the robot state and operator commands using a learned safety critic $Q^\text{safety}$, intervening only when the proposed action would violate safety constraints. Rather than issuing aggressive overrides, the system computes the *closest safe action* to minimize disruption during shared autonomy.

<div class="row justify-content-sm-center">
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid
      path="assets/img/isaacs-information-structure.png"
      title="ISAACS information structure in training and deployment"
      class="img-fluid rounded z-depth-1" 
      style="height: 250px; object-fit: scale-down;"
    %}
  </div>
  <div class="col-sm-7 mt-3 mt-md-0">
    {% include figure.liquid
      path="assets/img/value-based-shielding-block-diagram.png"
      title="Value-based shielding block diagram"
      class="img-fluid rounded z-depth-1"
      style="height: 250px; object-fit: scale-down;"
    %}
  </div>
</div>
<div class="caption">
  <b>Figure:</b> Online safety critic filter (value-based shielding) information flow and block diagram.
</div>

---

## Learning-Based Safety Filtering

The Safety Enforcer policy was trained using an adversarial reinforcement learning framework inspired by ISAACS {% cite pmlr-v211-hsu23a %}, allowing the system to reason over worst-case disturbances while optimizing safe behavior.

Unlike rule-based safety layers, the learned policy captures nonlinear interactions between robot dynamics, terrain geometry, and control actions.

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid
        loading="eager"
        path="assets/img/gvr-training-sim.gif"
        title="GVR training in simulation with force adversaries"
        class="img-fluid rounded z-depth-1" 
        style="height: 400px; object-fit: cover;"
        %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid
        loading="eager"
        path="assets/img/gvr-learn-flippers.gif"
        title="GVR learned to use flippers in simulation"
        class="img-fluid rounded z-depth-1" 
        style="height: 400px; object-fit: cover;"
        %}
    </div>
</div>
<div class="caption">
  <b>Figure:</b> The Safety Enforcer trained in simulation with ISAACS. Adversarial agent is modeled as external force applied to the robot (left), and the robot learned to use flippers to dampen the fall on wedge terrain (right).
</div>

---

## Featured Results: Wedge Terrain Traversal

The wedge terrain represents a high-risk scenario involving large angle variations and potential slam events. With LINC enabled, the robot automatically modulates flipper angles and forward velocity, allowing the operator to command high-level intent (e.g., maximum forward speed) while maintaining safety.

<div class="row justify-content-sm-center">
    <iframe width="800" height="450" src="https://www.youtube.com/embed/32XNHcQ8_ag?si=RG0N-hlO_zTXR5Yy" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>
<div class="caption">
  <b>Video:</b> Learned Safety Enforcer enabling surprise-free shared autonomy during wedge traversal.
</div>

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid
      loading="eager"
      path="assets/img/wedge terrain - flippers action snapshots.png"
      title="DARPA LINC GVR robot on wedge terrain - snapshot"
      class="img-fluid rounded z-depth-1" 
      style="height: 350px; width: 100%; object-fit: cover; object-position: center;"
    %}
  </div>
</div>
<div class="caption">
  <b>Figure:</b> Sequence of snapshots showing our LINC Safety Enforcer’s automatic modulation of flippers on the wedge terrain (inline pass) when the operator is applying a maximum forward velocity command: (1) the robot moves towards the tipping point at the top of a wedge (2) LINC slows down the robot at the tipping point and lowers its flippers (3) LINC allows the robot to proceed forward, and flippers smoothly make contact with the terrain (4) LINC slows down the robot and brings flippers up (5) LINC allows robot to continue moving forward (6) LINC brings flippers down in anticipation of a possible upcoming tipping point.
</div>

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid
      path="assets/img/wedge terrain - pitch angle.png"
      title="Automatic flipper modulation during wedge traversal"
      class="img-fluid rounded z-depth-1" 
    %}
  </div>
</div>

<div class="caption">
    <b>Figure:</b> Evolution of the robot’s pitch angle (top) and pitch angular velocity (bottom) in two representative runs of the inline wedge terrain with LINC off and LINC on. By automatically controlling the flippers, LINC prevents the robot’s nose from dipping far below the horizon (pitch angle remains mostly positive) and keeps the angular velocity from reaching large values. Without LINC, the robot acquires an excessive angular velocity as it traverses ridges, culminating in slam events (red circles) in which this angular velocity drops abruptly to zero as the robot’s tracts impact the downward slope.
</div>

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid
      path="assets/img/wedge terrain - flippers action representative run.png"
      title="Wedge terrain - Flippers action of representative run"
      class="img-fluid rounded z-depth-1" %}
  </div>
</div>

<div class="caption">
    <b>Figure:</b> Automatic control of flippers by the LINC Safety Enforcer during a representative run of the wedge terrain. LINC lowers the flippers as the robot approaches and traverses a ridge, preventing slam events and keeping the nose from dipping significantly below the horizon, which results in smoother and faster traversal. As the robot transitions onto the next upward slope, LINC raises the flippers, preventing an unnecessary growth in the pitch angle. Note that the <u>LINC controller has no map of the terrain and uses only the robot’s estimated state</u>.
</div>

---

## Additional Scenarios: Single-Track Incline
On steep inclines, the Safety Enforcer prevents toppling by modulating forward velocity and halting motion when safety thresholds are exceeded. Operators can adjust acceptable risk levels to continue traversal when appropriate.

<div class="row justify-content-sm-center">
    <iframe width="800" height="450" src="https://www.youtube.com/embed/Mt06o7aKx1k?si=f4h_BBDvu10x8o16" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>
<div class="caption">
  <b>Video:</b> Learned Safety Enforcer enabling surprise-free shared autonomy during single-track incline terrain.
</div>

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid
      path="assets/img/single-track incline - stopping.png"
      title="Single-track incline - stopping with high setpoint"
      class="img-fluid rounded z-depth-1" 
    %}
    {% include figure.liquid
      path="assets/img/single-track incline - nudging.png"
      title="Single-track incline - nudging with low setpoint"
      class="img-fluid rounded z-depth-1" 
    %}
  </div>
</div>

<div class="caption">
    <b>Figure:</b> Automatic modulation of forward speed by the LINC Safety Enforcer on the single-track incline during representative runs with high and low setpoint. In the high-setpoint run (top), LINC brings the robot to a halt before it tips over; eventually, the operator backs out and takes an alternative route. In the low-setpoint run (bottom), LINC gradually restricts the allowable speed as the robot approaches the top of the incline, and then allows it to speed up along the downslope. The green shading indicates times at which the Safety Enforcer is intervening.
</div>

---

## Final Field Test: Unified Safety Enforcer

In the final evaluation, a **single unified Safety Enforcer** was deployed across all terrains without mode switching. The system remained robust even under **unmodeled disturbances**, including a pendulum payload attached to the robot.

<div class="row justify-content-sm-center">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid
      path="assets/img/linc-phase0-full-track.png"
      title="Final test snapshots across terrains"
      class="img-fluid rounded z-depth-1"
      style="height: 240px; width: 100%; object-fit: cover; object-position: center;"
    %}
  </div>
</div>
<div class="caption">
  Sequence of snapshots from the final field test demonstrating safe traversal across diverse terrains with a single learned safety policy.
</div>

---

## Takeaways

This project demonstrates how learning-based safety mechanisms can be:
- **Effective:** preventing failure modes such as toppling, slamming, and collisions
- **Human-centered:** preserving operator intent with minimal, predictable intervention
- **Robust:** generalizing across terrains and unmodeled disturbances

The techniques developed here inform my broader research on safe reinforcement learning and real-world deployment of autonomous systems.