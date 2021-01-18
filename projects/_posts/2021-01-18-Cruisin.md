---
layout: projects
title: Visual Odometry Pipeline
tag: Computer Vision
description: Localizing/mapping the trajectory of a moving vehicle with only a camera.
tools: OpenCV
img: Media/blog/vo/fast-corners.png
---
<img src="/Media/blog/vo/fast-corners.png">
*Unrelated: sample image of the FAST corner detection algorithm*

**Summary**: I wrote an algorithm to localize/map the position of a vehicle using a single camera mounted to it. This is known as *monocular visual odometry*.

In early 2020, I decided to start a very ambitious (longterm) side-project. I won't spill the idea just yet, but it's a computer-vision based project for cars. Between school and internships, I haven't had a ton of time to dedicate to it recently, but I wanted to show one aspect that I implemented and that took a lot of learning on my part.

<video controls src="/Media/blog/vo/visual-odometry1.mov" width="100%">
    Sorry, your browser doesn't support embedded videos.
</video>
*Left: estimated position of vehicle, Right: input to my pipeline*

<video controls src="/Media/blog/vo/visual-odometry2.mov" width="100%">
    Sorry, your browser doesn't support embedded videos.
</video>

Ideally, the algorithm would be supplemented by other inertial, visual and/or GPS sensors. This is part of a much larger project that is still under development, so progress updates are very likely!