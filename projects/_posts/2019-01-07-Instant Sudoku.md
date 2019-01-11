---
layout: projects
title: Instant Sudoku
tag: Flask, webapp, CV, ML
description: Made a webapp that uses CV to solve sudoku puzzles in the browser.
img: Media/kachow.PNG
tools: Sci-kit Learn (ML classifiers), Flask (backend web dev), Heroku (server deployment), OpenCV
img2: yeet
---
### A demo for this project is live as a webapp <a href="https://instant-sudoku.herokuapp.com">here</a>

Last year I started working on a project that would enable me to learn more about ML classifiers. The project consisted of a script that would use some computer vision heuristics to extract important information from a user-provided sudoku game. It would then implement a classifier to recognize digits in the puzzle, based on training data that I collected myself.
<img src="/Media/sudoku_recognition.png" style="size: 50%;">

As you can see, it was not too bad for a first attempt. I let that project sit for a while as I started my first semester at university and I recently put aside enough time to complete this project. I managed to increase accuracy of the classifier by increasing the size of my dataset as well as playing around with different classifier types (KNN, logistic regression, SVM).
<img src="/Media/training_example.PNG">

Finally, I incorporated the project into a complete web application. It allows a user to upload a picture of a printed sudoku game, recognizes the puzzle, solves it, then displays the solution (if one exists).




