---
layout: projects
title: A Simple Line Detection Algorithm in Python
tag: Tutorial, Python, OpenCV, Numpy
description: A helpful guide for someone wanting to learn how to use OpenCV
tools: Python, OpenCV, Numpy
img: /Media/blog/lineDetection/output_17_1.png
---
<img src="/Media/blog/lineDetection/output_17_1.png">
In this post, I want to show you how easy it is to write a simple computer vision script. In this example, I'll go over the application of road line detection. Obviously, there are many additional steps to make this functional for say, an autonomous vehicle, but hopefully this can help get you started.

You will first need to make sure you have the following installed:
- Python 3
- OpenCV 
- numpy

(These can easily be installed using pip).

Note: I'm using jupyter notebooks to create this tutorial, for this reason I'm using matplotlib to display the images. This is generally unnecessary for most applications, so you should use **cv2.imshow("NAME", image)**

So, let's start by importing these libraries:


```python
# modules for *MY* setup:
%matplotlib inline
import matplotlib
from matplotlib import pyplot as plt

# important modules:
import cv2
import numpy as np
```

Now, let's try accessing an image. I have a file called "road lines.jpg" in my project directory


```python
img_bgr = cv2.imread("road lines.jpg")

img_rgb = cv2.cvtColor(img_bgr, cv2.COLOR_BGR2RGB)

# cv2.imshow("road image", img)
plt.imshow(img_rgb)
```


<img src="/Media/blog/lineDetection/output_3_1.png">


Great! Now to more complex stuff. Let's try changing the *color space* of our image. There are many color spaces to choose from; common examples are RGB, BGR, HLS, etc. 

For the sake of this tutorial, let's try HLS:


```python
# We use the cvtColor function from opencv
# The parameters are: initial image and conversion
img_hls = cv2.cvtColor(img_bgr, cv2.COLOR_BGR2HLS)

# cv2.imshow("road image", img)
plt.imshow(img_hls)
```


<img src="/Media/blog/lineDetection/output_5_1.png">


Ok, it obviously looks different

Now, let's start some line detection!
The first step would be to focus on the yellow road lines, so let's extract that:


```python
# Here, we define a range of colors that satisfy the color yellow:

# let's try with both a BGR and an HLS color range
bgr_mask = cv2.inRange(img_bgr, (0, 137, 158), (145, 255, 251));
hls_mask = cv2.inRange(img_hls, (20, 120, 80), (45,200,255));
```

Let's plot both of our masks


```python
plt.imshow(hls_mask)
```


<img src="/Media/blog/lineDetection/output_9_1.png">



```python
plt.imshow(bgr_mask)
```


<img src="/Media/blog/lineDetection/output_10_1.png">


Looks like both of these worked. Obviously, we could just proceed with use the HLS mask since it turned out so nice, but in order to have the best possible image, let's put both of these together:


```python
mask = bgr_mask | hls_mask
plt.imshow(mask)
```


<img src="/Media/blog/lineDetection/output_12_1.png">


Much better! Here, we probably don't need to, but let's try _eroding_ the image

```python
kernel = cv2.getStructuringElement(cv2.MORPH_RECT,(5,5))
eroded = cv2.erode(mask, kernel, iterations = 3)

plt.imshow(eroded)
```


<img src="/Media/blog/lineDetection/output_14_1.png">


```python
output_img = np.copy(img_rgb)

lines = cv2.HoughLinesP(eroded, 0.8, np.pi/180, 100, np.array([]), 
	minLineLength=100, maxLineGap=200)
for x1,y1,x2,y2 in lines[:, 0]:
    cv2.line(output_img, (x1,y1), (x2, y2), (255, 0, 0), 20)
    
plt.imshow(output_img)
```


<img src="/Media/blog/lineDetection/output_15_1.png">


Something useful you can do now is separate the right road-line from the left road-line.

A simple way to do that would be to look at the slope of the lines. You can clearly see that due to the perspective of the camera, the left road line has a positive slope, while the right road line has a negative slope. 
We can use some high school math to figure this out:

$$m = \frac{\Delta y}{\Delta x}$$


```python
output_img = np.copy(img_rgb)

lines = cv2.HoughLinesP(eroded, 0.8, np.pi/180, 100, np.array([]), 
	minLineLength=100, maxLineGap=200)

for x1,y1,x2,y2 in lines[:, 0]:
#   To avoid the case of dividing by zero:
    if (x2-x1 == 0):
        m = 9999
#   Calculating slope
    else:
        m = (y2 - y1)/(x2 - x1)
#   Separating the lines by color
    if(m > 0):
        cv2.line(output_img, (x1,y1), (x2, y2), (255, 0, 0), 20)
    if(m < 0):
        cv2.line(output_img, (x1,y1), (x2, y2), (0, 0, 255), 20)

plt.imshow(output_img)
```



<img src="/Media/blog/lineDetection/output_17_1.png">

Congratulations! You have just written your first computer vision script in python! If you have any questions, do not hesitate to reach out to me!

