---
layout: projects
title: Line Follower Robot
tag: Robotics
description: Fast/light differential drive robot for figurine rescue competition.
tools: C, 8-bit MCU, soldering
img: Media/projects/line_follower/line_follower_render.png
---

In a recent course at UWaterloo (MTE380), we were tasked with designing and building a search and rescue robot to compete against the rest of our class. The competition was tight, with teams being judged on their robot's speed and weight for a price-constrained solution, all while having to rescue a LEGO minifigure autonomously on an unknown course.
<video autoplay loop muted playsinline>
 <source src="/Media/projects/line_follower/driving.mp4" type="video/mp4">
</video>
*Our robot on the final course (note: clip sped up)*

The whole project was pretty open-ended and no one really knew what the course would look like. Originally, we started with the design shown below. It was a differential drive robot, relying mainly on an infrared reflectance sensor array for line following. Most teams were using some kind of claw/gripper to grab and release the LEGO figure - although you can see we decided to try making an ejectable adhesive-covered bumper. This helped us to significantly reduce weight and improve reliability.
<img src="/Media/projects/line_follower/alternate-design-render.png">
*Original design render*

That design was used as a testbench to develop simulations for our control system, mainly validated using MATLAB. Although, we decided that we wanted to aggressively reduce the mass of our robot to (1) make our kinetic-less simulations more representative, (2) be more efficient, and (3) optimize for design points. The final design is shown below: 

<img src="/Media/projects/line_follower/line_follower_render.png">
*Final design render*

Some notable changes:
- Rack and pinion bumper ejector -> traded for crank-slider
- 2-level acrylic chassis -> everything mounted on single circuit board 
- STM32 Nucleo -> Arduino Pro Mini (not much compute needed anyways)
- IR array -> color sensors

In the end, our robot was substantially lighter than the other solutions at 142g with a best completion time of 45 seconds.

