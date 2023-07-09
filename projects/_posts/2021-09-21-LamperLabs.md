---
layout: projects
title: Bio-mimetic Fish Robot
tag: Robotics
description: Design of a Bio-mimetic robot platform for marine ecology research
tools: 
img: Media/projects/lamperlabs/lamper_assembly.png
---
<img src="/Media/projects/lamperlabs/lamper_assembly.png">
*SolidWorks assembly*

<a href="https://lamperlabs.github.io/">LamperLabs</a> was a project focused on developing a fish-like robotic platform capable of gathering data in shallow water environments (ie: aquarium tanks and calm bodies of water). I co-founded the team with 3 friends and we managed to get backing from the Engineer of the Future Fund at UW to build a prototype.

## Architecture
<img src="/Media/projects/lamperlabs/lamper-hw-block-diagram.png">
*Hardware overview*

The robot itself was architected around the Nvidia Jetson single-board computer with an auxiliary microcontroller to handle actuator control requests asynchronously. These requests originate from a running websocket connection that relies on the fish's tethered WiFi receiver above water. Meanwhile, the Jetson captures video through the CSI2 camera, producing an RTP stream (via Gstreamer) with frames coming directly from the DMA buffer for very high throughput.

## Propulsion
<video autoplay loop muted playsinline>
 <source src="/Media/projects/lamperlabs/lamper-build.mp4" type="video/mp4">
</video>
*Propulsion system demos*

I worked with our mechanical lead (Kyle) closely to push for a single-motor propulsion system. As the motor completes a full revolution, the custom gear box transfers torque to two oppositely rotating turntables. Wires routed through the ribs of the tail are subject to alternating tension and slack to produce a tuna-like swimming pattern. I mainly helped with back-of-the-envelope mechanism sketches and kinematic modeling, while Kyle produced the actual CAD.

I also learned how to use SolidWork's hydrodynamics FEA tools as we wanted to estimate the pressure that our sealant would need to withstand given certain conditions:
<img src="/Media/projects/lamperlabs/lamper-pressure1.png">
*Pressure due to hydrodynamic forces*

## Custom SW Framework
Let me be the first to say that we wrote a metric ton of code for this project - a lot of which was from scratch. In total, there were three code bases that our team maintained:
1. LamperCloud: Web app to control and view the fish's POV in real-time [Owner: Kiran]
2. Nemo: Multi-threaded program that lives on the Nvidia Jetson [Owner: Me]
3. Dori: Auxiliary microcontroller's firmware [Owner: Dhruv]

<img src="/Media/projects/lamperlabs/lamper-cloud.png">
*Web app for controlling and viewing fish POV in real-time*

I focused on Nemo, which was a multi-threaded program written in C for the Nvidia Jetson. It carries out the video streaming pipeline to LamperCloud, receives robot controls over websockets, and sends motor commands to the auxiliary controller over UART. Looking back - an insane amount of work went into this.

<img src="/Media/projects/lamperlabs/nemo-block-diagram.png">
*Nemo block diagram*