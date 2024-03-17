---
layout: projects
title: Meals on Wheels, Racing Robot
tag: Robotics
description: A self-driving race car
tools: Embedded computer, Python, OpenCV, Arduino, ESC 
# img: /Media/projects/iarrc1/AutonomousCar.gif
video: /Media/projects/iarrc1/AutonomousCar.mp4
---
In 11th grade, I wanted to step up my robotics know-how so I founded a robotics team and taught myself classical computer vision concepts. 

To give ourselves an ambitious challenge, I entered the team into the International Autonomous Robot Racing Challenge (IARRC) -- an annual event where university design teams compete to design a self-driving robot. As far as I know, we were the only highschool team participating that year against teams like UWaterloo, Georgia Tech, Western University, KMUTT, etc. We did quite well and placed second -- beat only by my future university's team.

<video autoplay loop muted playsinline>
 <source src="/Media/projects/iarrc1/AutonomousCar.mp4" type="video/mp4">
</video>
*Meals on Wheels navigating a test track* 

The robot relies on a front-facing camera feed processed by a raspberry pi to understand the world around it. Geometrical computer vision techniques allowed for the robot to accurately detect roadlines and navigate the track accordingly.

<img src="/Media/projects/iarrc1/car1.jpg">
*Render*

Especially compared to other teams, our hardware/mechanical was quite scrappy. We basically stripped down a RC car and bolted a cooking tray to it as our main chassis. That's why we named the car "Meals on Wheels".
