---
layout: projects
title: Vision-Based Piano Transcriber
tag: Computer Vision
description: Using CV to turn video into music.
tools: Python, OpenCV, Lily
img: Media/SharpMusicPanel.png
---
<img src="/Media/sharpmusic-thumbnail.jpg">

This project was built for JamHacks 2018 (highschool hackathon). It was built with Lyne Baaj and Danny Ou in 24 hours.

At the hackathon, we noticed a piano sitting in one of the main areas. It was an old piano with some missing keys, but we tried playing it anyways. Predictably, it sounded horrible as most of the keys were completely out of tune. The only way to guess what song we were playing was to watch the keys we pressed — definitely not by listening.

Most transcription software works by interpreting audio signals, so we asked ourselves: could we make our own transcription system that uses video instead? The answer was yes! We spent our time at the hackathon doing research and building SharpMusic — the computer vision based music transcription system.

SharpMusic works by placing a normal webcam in front of a piano so that it can see the key faces and our program will do some processing to extract the necessary information. 
<img src="/Media/sharpmusic-key-detection.jpg">
*Early stages of the key detection*

Once the keys are detected, the user can begin playing notes and the sheet music will be generated after the session.

<img src="/Media/sharpmusic.gif">
*Note detection and sheet music generation demo*

In the future I plan to make this concept more practical by using an overhead view of the piano in order to capture more of the piano's keys and to avoid interference with the composer. Moreover, I would like to continue working on the computer vision script to make it more robust and eventually create a full GUI for this proof of concept.