---
layout: page
title: DARPA LINC Phase 1
description: Learning Introspective Control for Replenishment at Sea missions.
img: assets/img/linc-crane-helicopter-short.gif
importance: 3
category: work
# related_publications: true
selected: true
---

<div class="row justify-content-sm-center">
  <div class="col-sm-3 mt-3 mt-md-0">
    {% include figure.liquid
      path="assets/img/crane-on-motion-platform-brg.jpg"
      title="ISAACS information structure in training and deployment"
      class="img-fluid rounded z-depth-1"
      style="height: 300px; object-fit: cover;" %}
  </div>
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid
      path="assets/img/crane-on-motion-platform-brg-short-speedup.gif"
      title="Value-based shielding block diagram"
      class="img-fluid rounded z-depth-1"
      style="height: 300px; object-fit: cover;" %}
  </div>
</div>
<div class="caption">
  <b>Figure:</b> LINC for Replenishment at Sea mission, developed for robotic crane system.
</div>


In **DARPA LINC Phase 1**, we scaled the core ideas from Phase 0 to a significantly more challenging setting in safe autonomy and human–robot interaction: developing a **Learning Introspective Control (LINC)** system for **Crane-on-Ship Replenishment at Sea** operations.

Under a range of adversarial conditions, including a moving platform simulating aggressive sea states, close-proximity obstacles, and degraded actuator performance, our approach maintains bounded payload oscillations while enabling a human operator to intuitively control the crane. This allows the payload to be maneuvered reliably and inserted into assigned goals despite disturbances.

<div class="row justify-content-sm-center">
    <iframe width="800" height="450" src="https://www.youtube.com/embed/syAuVlm0bjc?si=xgpZYRatV3UPhf79" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>
<div class="caption">
    <b>Video:</b> Under adversarial scenarios, including simulated sea motion, nearby obstacles, and actuator degradation, LINC supports a human operator in smoothly controlling payload motion and successfully completing replenishment tasks.
</div>

To stress-test the system, the 6-DoF motion platform was commanded to induce highly aggressive sea states. When LINC is disabled, the injected energy exceeds the system’s natural dissipation, resulting in chaotic, uncontrollable payload motion.

The video below demonstrates that our proposed method preserves controllability and stability even in these extreme conditions, allowing a human-operated crane to complete a replenishment task safely and effectively.

<div class="row justify-content-sm-center">
    <iframe width="800" height="450" src="https://www.youtube.com/embed/31k6ptfBM4U?si=5PxvTFNWE6CA0FYQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>
<div class="caption">
    <b>Video:</b> Comparison of LINC on (left) and LINC off (right) during payload insertion under adversarial disturbances induced by a 6-DoF motion platform. While aggressive sea states generate uncontrollable cyclic motion without assistance, LINC bounds oscillations and enables successful payload insertion into the target goal.
</div>