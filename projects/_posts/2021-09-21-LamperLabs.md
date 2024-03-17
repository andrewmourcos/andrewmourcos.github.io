---
layout: projects
title: Lamper, Robot Platform
tag: Robotics
description: A bio-inspired robot platform for marine ecology research
tools: 
img: Media/projects/lamperlabs/lamper_assembly.png
video: /Media/projects/lamperlabs/lamper-land-test.mp4
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

A big mechanical challenge was in designing a single-motor propulsion system, led by my friend Kyle Tam. It definitely made the project more complex, but allowed us to produce an accurate fish swimming stroke, lower actuator costs and achieve the best mechanical efficiency. As the motor completes a full revolution, the custom gear box transfers torque to two oppositely rotating turntables. Wires routed through the ribs of the tail are subject to alternating tension and slack to produce a tuna-like swimming pattern.

Also took this project as an excuse to use FEA tools when we wanted an estimate of hydrodynamic pressure the fish would need to withstand.
<img src="/Media/projects/lamperlabs/lamper-pressure1.png">
*Pressure due to hydrodynamic forces*

## Software
Let me be the first to say that we wrote a metric ton of code for this project - a lot of which was from scratch. In total, there were three code bases that our team maintained:
1. LamperCloud: Web app to control and view the fish's POV in real-time [Owner: Kiran]
2. Nemo: Multi-threaded program that lives on the Nvidia Jetson [Owner: Me]
3. Dori: Auxiliary microcontroller's firmware [Owner: Dhruv]

<img src="/Media/projects/lamperlabs/lamper-cloud.png">
*Web app for controlling and viewing fish POV in real-time*

I focused on Nemo, which was a multi-threaded program written in C/C++ for the Nvidia Jetson. It carries out the video streaming pipeline fed to LamperCloud, receives robot controls over websockets, and sends motor commands to the auxiliary controller over UART.

<img src="/Media/projects/lamperlabs/nemo-block-diagram.png">
*Nemo block diagram*