---
layout: page
title: ISAACS and Gameplay Filters
description: Safety Filter synthesis and deployment for high-order dynamical systems
img: assets/img/robert-kicking-short-zoom.gif
importance: 1
category: work
related_publications: true
---

# ISAACS
ISAACS (Iterative Soft Adversarial Actor-Critic for Safety) {% cite pmlr-v211-hsu23a %} is a new game-theoretic reinforcement learning scheme for approximate safety analysis, whose simulation-trained control policies can be efficiently converted at runtime into robust safety-certified control strategies, allowing robots to plan and operate with safety guarantees in the physical world.

<div class="row justify-content-sm-center">
    <iframe width="800" height="450" src="https://www.youtube.com/embed/RlPQR044pEQ?si=cEpnkozxuI7I2hsS" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>
<div class="caption">
  <b>Video:</b> Synthesis and runtime of safety critic filter with ISAACS on quadruped robot.
</div>

# Gameplay Filters

<div class="row justify-content-sm-center">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid
      loading="eager"
      path="assets/img/corl-gameplay-frontFigure3.jpg"
      title="Gameplay Filters front figure"
      class="img-fluid rounded z-depth-1" 
      style="height: 300px; width: 100%; object-fit: cover; object-position: center;"
    %}
  </div>
</div>
<div class="caption">
  <b>Figure:</b> Snapshots of two different quadruped robots under adversarial conditions, including external tugging forces and unmodeled terrains. The gameplay filter preserves safety across experiments, compared to the unfiltered counterpart.
</div>

The <b>gameplay filter</b> {% cite nguyen2024gameplay %} is a new class of predictive safety filters, offering a general approach for runtime robot safety based on game-theoretic reinforcement learning and the core principles of safety filters. Our method learns a best-effort safety policy and a worst-case sim-to-real gap in simulation, and then uses their interplay to inform the robot’s real-time decisions on how and when to preempt potential safety violations.

---

## Learn from adversity

<div class="row">
  <div class="col-sm-8 mt-3 mt-md-0">
    Our approach first pre-trains a safety-centric control policy in simulation, by pitting it against an adversarial environment agent that is simultaneously learning to steer the robot towards catastrophic failures. This escalation produces a robust robot safety policy that is remarkably hard to exploit, but also an estimate of the worst-case sim-to-real gap that the robot might encounter after deployment. The algorithm updates a safety value network (critic) and keeps a leaderboard of the most effective player policies (actors).
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid
      loading="eager"
      path="assets/img/rss-spirit-training.gif"
      title="RSS Spirit training in simulation"
      class="img-fluid rounded z-depth-1" 
    %}
  </div>
</div>

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid
      loading="eager"
      path="assets/img/isaacs-training-process.png"
      title="ISAACS training process"
      class="img-fluid rounded z-depth-1" 
    %}
    <div class="caption">
      <b>Synthesis</b>: We employ a game-theoretic reach-avoid reinforcement learning scheme that iteratively pits the robot's controller against a simulated adversarial environment. The algorithm updates a safety value network (critic) and keeps a <i>leaderboard</i> of the most effective player policies (actors).
    </div>
  </div>
</div>

---

## Never lose a game

At runtime, the learned player strategies become part of a safety filter, which allows the robot to pursue its task-specific goals or learn a new policy as long as safety is not in jeopardy, but intervenes as needed to prevent future safety violations. 

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid
      loading="eager"
      path="assets/img/gameplay-filter-deployment-diagram.png"
      title="Gameplay Filters deployment diagram"
      class="img-fluid rounded z-depth-1" 
    %}
    <div class="caption">
      <b>Runtime</b>: Our gameplay filter maintains safety by continually playing out imagined safety games between the best learned controller and disturbance. It <b><i>only</i></b> blocks task-driven actions that could lead to losing future games (i.e., violating safety) and replaces them with the learned safety controls.
    </div>
  </div>
</div>

To decide when and how to intervene, the gameplay filter continually imagines (simulates) hypothetical games between the two learned agents after each candidate task action: if taking the proposed action leads to the robot losing the safety game against the learned adversarial environment, the action is rejected and replaced by the learned safety policy.

---
## Results

### 1. Tugging Forces and Irregular Terrain Evaluation
We evaluate the Gameplay Filters on two quadruped robot platforms, Unitree Go2 and Ghost Robotics S40, across two experimental settings:

* **Matched ODD (50 N tugging force)**: A disturbance consistent with the training Operational Design Domain (ODD), designed to assess whether the Gameplay Filter can maintain robust safety without excessively hindering task execution.
* **Unmodeled terrain**: A deployment scenario outside the training distribution, used to evaluate whether the Gameplay Filter can preserve zero-shot safety under unmodeled conditions.

**Gameplay filter on unmodeled terrain**
<div class="row justify-content-sm-center">
    <iframe width="800" height="450" src="https://www.youtube.com/embed/cjRP93HAkDQ?si=2F3o4I_H6jh6IYDT" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>
<div class="caption">
  <b>Video:</b> Gameplay Filter on bumpy terrain experiment.
</div>

**Gameplay filter under tugging force**
<div class="row justify-content-sm-center">
    <iframe width="800" height="450" src="https://www.youtube.com/embed/hPhStA7SzmQ?si=zlALtt29NeJ2M37l" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>
<div class="caption">
  <b>Video:</b> Gameplay Filter against tugging force experiment.
</div>

**Baseline comparison: Safety critic filter and unfiltered task policy**
<div class="row justify-content-sm-center">
    <iframe width="800" height="450" src="https://www.youtube.com/embed/18CS0Wcbjmk?si=3mbaYSRtmI0WD8TV" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>
<div class="caption">
  <b>Video:</b> We compare the result of gameplay filter against 2 baselines: Safety critic filter, and unfiltered task policy. Across all experiments, the gameplay filter maintains higher safe rate, and only fail when the adversarial bound exceeds the defined ODD.
</div>

### 2. Implicit robustness against degradation
In this demonstration, the rear right abduction motor was broken. The robot's task policy and safety filter were unaware of this.
<div class="row justify-content-sm-center">
    <iframe width="800" height="450" src="https://www.youtube.com/embed/P2bFGkKamnQ?si=SFZipKgcnIPDPRlL" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>
<div class="caption">
  <b>Video:</b> A demonstration showing gameplay filter maintaining safety for the robot with broken motor (rear right abduction) while under tugging force. This highlights the effectiveness of the method, with implicit robustness against degradation.
</div>

Similarly, when the motors of the Unitree Go2 were <b><u>noticeably degraded</u></b>, with incorrect encoder readings and dampened actuation performance during the CoRL 2024 demo, the manufacturer's built-in controller could no longer stabilize the robot, causing it to fail on its own.

Despite this, our Gameplay Filters solution continued to function, <b><u>demonstrating strong robustness to real-world degradation and adversarial conditions</u></b>.

<div class="row justify-content-sm-center">
    <div class="col-12 mt-3 mt-md-0">
        <div class="row justify-content-center gx-3 gy-3">
            <div class="col-12 col-md-auto">
                <iframe width="400" height="225" src="https://www.youtube.com/embed/WQg4HhBZ3Nc?si=julaGm88f9kfLkl_" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
            </div>
            <div class="col-12 col-md-auto">
                <iframe width="400" height="225" src="https://www.youtube.com/embed/Nm4ev8VXWrE?si=gQ1zz-3NAGi0KeFV" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
            </div>
        </div>
    </div>
</div>
<div class="caption">
    <b>Video:</b> (Left) Manufacturer's built-in controller causes robot from falling by itself after motor and sensor degradation. (Right) Gameplay filter allows the robot to still function safely.
</div>

### 3. Tackling large sim-to-real gap
In this demonstration, we train and deploy an RL-driven locomotion task policy on the Unitree Go2 robot with large sim-to-real gap. When deployed on the robot, the task policy causes the robot to flip over. Deploying gameplay filter allows the robot to complete the sequence of task actions without falling.

<div class="row justify-content-sm-center">
    <div class="col-12 mt-3 mt-md-0">
        <div class="row justify-content-center gx-3 gy-3">
            <div class="col-12 col-md-auto">
                <iframe class="d-block mx-auto" width="400" height="225" src="https://www.youtube.com/embed/hHTRdW3too4?si=W_sV0snn3tyHGdXs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
            </div>
            <div class="col-12 col-md-auto">
                <iframe class="d-block mx-auto" width="400" height="225" src="https://www.youtube.com/embed/IxLHCLyvl8k?si=5yYJNomF2O9v7j0R" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
            </div>
        </div>
    </div>
</div>
<div class="caption">
    <b>Video:</b> Sim-to-real deployment of an RL-trained locomotion policy on the Unitree Go2. Due to a large sim-to-real gap, the unfiltered policy causes the robot to flip during execution (left). When augmented with the Gameplay Filter, the robot successfully completes the task sequence without falling (right). 
</div>

---

## Takeaway
Gameplay filters allow robots to maintain robust zero-shot safety across deployment conditions with minimal impact on task performance.

<ul>
    <li style="list-style-type: '✅  '">It only overrides unsafe actions that would cause a safety failure for some realization of uncertainty.</li>
    <li style="list-style-type: '✅  '">Only requires a single trajectory rollout at each control cycle, enabling runtime safety filtering.</li>
    <li style="list-style-type: '✅  '">To our knowledge, this is the first successful demonstration of a full-order safety filter for legged robots (36-D).</li>
</ul>

**Key contributions:**
- <b>Scalable</b>: The filter’s neural network makes it suitable for challenging robotic settings like walking on abrupt terrain and under strong forces.
- <b>General</b>: A gameplay filter can be synthesized automatically for any robotic system. All you need is a (black-box) dynamics model.
- <b>Robust</b>: The gameplay filter actively learns and explicitly predicts dangerous discrepancies between the modeled and real dynamics.