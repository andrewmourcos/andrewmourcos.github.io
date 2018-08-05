---
layout: projects
title: Meals on Wheels
tag: Embedded systems, Robotics, Computer Vision
description: A camera-based autonomous race car, made with rudimentary hardware found around the house. Made with the goal of promoting research in autonomy for younger students.
tools: Embedded computer, Python, OpenCV, Arduino, ESC 
img: Media/car1.png
img2: <img src="/Media/AutonomousCar.gif">
img3: <iframe src="/Media/IARRCCTV.mp4"></iframe>
---

My highschool had not had a robotics team for over 6 years, so in my junior year, I decided to found *Cavalier Robotics* to share my passion with others from my school. Now, the team needed a purpose so I searched for competitions that we could compete in. One in particular caught my attention: the *International Autonomous Robot Racing Challenge*. This is a university-level competition hosted at the University of Waterloo. 

By the end of the school year, we were able to build this robot which used a single-board computer as the main processor. Frames captured from a front-facing camera and a couple ultrasonic sensors were used as inputs for an algorithm I constructed. The architecture of the algorithm is as follows:
1. Detect traffic light state (has the race begun?)
2. Perform roadline detection
3. Utilize roadlines for localization
3. Determine best course of action (using PID)
4. Send driving decision via serial to microcontroller

In the end, our car worked the best and the algorithm proved to be quite robust, as we won 2nd place as the only highschool team participating.