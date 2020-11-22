---
layout: projects
title: PCB Etching with Vinegar+Peroxide?
tag: Experiment
description: A while ago I came across an article stating that it may be possible to etch PCBs from household chemicals and I decided to give it a shot.
tools: 
img: /Media/blog/vinegar_etching/blue_halfway.JPG
---
**TLDR: fun experiment, I'm not a chemist, mystery debunked**

<img src="/Media/blog/vinegar_etching/blue_halfway.JPG">

My first experience etching a custom PCB was in grade 6 with a friend of mine when we wanted to make our own remote-controlled car. At the time, we came across someone on the internet who claimed they could etch a PCB using nothing but regular vinegar and peroxide. That sounded pretty cool, so we gave it our best shot in my kitchen and literally nothing happened.

Some years later (grade 11), I had started building my <a href="/projects/2017/09/01/Upcycled-3d-Printer.html">3d printer</a> and wanted to move the circuit from a breadboard onto a nice PCB. I had 2 FR4 copper-clad boards and the proper etchants to do the job (ferric chloride), but I did come across another person online who claimed they could use vinegar and peroxide (I think it might've been <a href="https://www.instructables.com/Make-a-Circuit-Board-With-Household-Goods/">this</a>).

I gave it a read and was interested when they said that they needed to add salt to catalyze the reaction (something we didn't try the first time). I had just finished my grade 11 chemistry course, where we learned about Le Chatelier's principle, so I was very interested in the explanation provided... So I gave it another shot!

<video controls src="/Media/blog/vinegar_etching/etch.mp4" width="100%">
    Sorry, your browser doesn't support embedded videos.
</video>

To my delight, a reaction did begin to occur after adding salt. It took a very long time (several hours), but the copper did start to etch away. There is a very nice chemistry discussion explaining what's happening <a href="https://chemistry.stackexchange.com/questions/102156/full-equation-when-using-vinegar-hydrogen-peroxide-and-salt-to-etch-copper?noredirect=1&lq=1">here</a>. An interesting effect is that the reaction produced a lot of foam (which I would promptly whisk away with a plastic knife).

<img src="/Media/blog/vinegar_etching/foam.JPG">

Sure, some copper began to etch off, but the question is: **can it etch a functional PCB? Unfortunately, my results say no.** I let the reaction take place over several hours and ultimately this just ruined the copper. It seems these chemicals could only etch off a small layer before oxidizing the board and halting the reaction.

*Disclaimer: mixing chemicals is generally a bad idea. I'm not a chemist, but I did take precautions such as ventilating the area, etc. I do not recommend anyone to try this.*



