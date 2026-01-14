---
layout: post
title: CoRL 2024 Demo Recap
date: 2024-11-08 00:00:00
description: Recap of everything that happened during CoRL 2024 Demo Session of Gameplay Filters
tags: demos
categories: research engineering
featured: true
related_publications: true
---

Live robot demos rarely go exactly as planned, and our CoRL 2024 demo was no exception.

The Gameplay Filters {% cite nguyen2024gameplay %} demo started with a setback: after the very first demo attempt on Day 1, the robot broke down. What followed was a full day of on-site debugging, tool borrowing from generous neighbors around the venue, and a lot of collective problem-solving under pressure. It was stressful, exhausting, and oddly bonding, all the things that come with running real robots in the wild.

Day 2 told a different story. With the robot back up and running, we were finally able to show the system as intended. The demo went smoothly, conversations with attendees flowed, and the experience became a reminder of why live demos, despite their risks, are so valuable.

This was my first time fixing a quadruped robot entirely from the inside out, under a serious time crunch. It was a huge confidence boost, and an experience I very much hope not to repeat.

This video is a short recap of that journey: the breakdowns, the fixes, the people who stepped in to help, and the small victory of getting a real system to work in a real conference setting. More than anything, it’s a snapshot of the teamwork and persistence behind the scenes of research demos.

<div class="row justify-content-sm-center">
    <iframe width="800" height="450" src="https://www.youtube.com/embed/gkrJvTnz4K8?si=WEITweypvJpoPSU4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>
<div class="caption">
  <b>Video:</b> CoRL 2024 Demo Recap
</div>

Interestingly, after the failure and repair, the robot’s legs were <b><u>noticeably degraded</u></b>, with incorrect encoder readings and dampened actuation performance. As shown in the video below, the manufacturer’s built-in controller could no longer stabilize the robot, causing it to fail on its own.

<div class="row justify-content-sm-center">
    <iframe width="800" height="450" src="https://www.youtube.com/embed/WQg4HhBZ3Nc?si=julaGm88f9kfLkl_" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>
<div class="caption">
  <b>Video:</b> Manufacturer's built-in controller causes robot from falling by itself
</div>

Despite this, our Gameplay Filters solution continued to function, <b><u>demonstrating strong robustness to real-world degradation and adversarial conditions</u></b>.