---
layout: projects
title: Table Tennis Robot
tag: Electronics
description: Practicing table tennis without breaking the bank
tools: Arduino
img: Media/ping-pong-robot/rally.MOV
---
<img src="/Media/ping-pong-robot/rally.MOV">
*The robot in action*

In high school, my friends and I played table-tennis *a lot*. After liberating our school's old (semi-broken) ping pong table from the depths of the storage closet, we started playing almost every day: during lunch, between classes, even after school! Ping-pong soon became very popular and our school bought 2 new tables because of it!

That's when I had the idea to make a so-called *ping-pong robot*. I saw that professional players would use these robots to practice their rallying. I wanted one, but I also didn't want to pay a lot of money for it... So instead, I built one!

The first version was pretty bare-bones. It consisted of a ball launcher (DC motor flimsily attached to a cardboard tube) and a ball holder with a servo motor as a timed "ball faucet". Even though it was simple, it served it's purpose.

For the second version, I had no need to upgrade the building material — cardboard worked great and costs nothing. However, I wanted to assemble it in a more robust way that required less tape :) as well as add a few new features. 

I split the contraption into two detacheable modules: the ball launcher and the ball feeder. The ball feeder consists of two cardboard tubes that join at a 90 degree angle. At that intersection, I have a servo motor acting as a piston. When it's time to fire a ball, the servo retracts an arm, a ball drops into the second tube and finally the servo extends the arm — pushing the ball into the launcher.

<img src="/Media/ping-pong-robot/feeder.MOV">
*Closeup of ball feeder*

The second version of the launcher didn't change drastically. It was still a cardboard tube with a wheel poking into one side to launch the ping pong balls (much like a motorized hot-wheels track). The two main differences were (1) better structural integrity and (2) being completely detacheable from the feeder. The reason for this is that I wanted to be able to attach the launcher in any orientation to change the direction of the spin it put on the ball. For example, if I wanted to practice against top-spin, I would orient the launcher upright; if I wanted backspin, I would rotate the launcher 180 degrees W.R.T. the feeder.

<img src="/Media/ping-pong-robot/controls.JPG">
*Image showing the controls and electronics stuffed in the project box*

Finally, I added some physical controls (potentiometers) for ball spin/range as well as for the launching rate. And, of course, you can change the spin direction by rotating the launcher.

Later, I made a CAD drawing for the next version of this project. The launcher will have 3 motors instead of 1 as that would allow me to control spin direction on the fly (instead of manually changing it). The idea is to make a "random" mode where it hits me with a sequence of different spin/speed types.
<img src="/Media/ping-pong-robot/cad.jpg">
*Concept CAD drawing for the next version — 3 motors to control spin*

All in all, a very practical project that I'm glad I built!

