---
layout: projects
title: IMU Sensor Fusion
tag: IMU guide
description: Explaining the limitations of angular positioning sensors and demonstrating the use of a complementary fusion algorithm.
tools: Accelerometer, Gyroscope
img: /Media/blog/imu/openlog.jpg
---
<img src="/Media/blog/imu/openlog.jpg">
So, you've just bought an inertial measurement unit (IMU) and you're trying to figure out how to get Euler angles from it. First, let's step back and figure out how an IMU actually works. 

An IMU is often a package of multiple sensors: accelerometer, gyroscope and magnetometer. For now, I'm going to ditch the magnetometer and focus on the first two.

<img src="/Media/blog/imu/plane_orient.png">
*This diagram shows the terminology often associated with orienting ones-self in space with an IMU*

## Gyroscopes
These are sensors that provide a measure of your angular speed. In other words, it will give us the "degrees/second" or $$\frac{d(angle)}{dt}$$. So, if we're just trying to use this sensor to tell us our pitch and roll angles, we need to integrate the values acquired from it. In pseudo-code/python, "integrating" would look like this:

~~~ python
while(True):
    dt = time.time() - last_time # don't actually use time.time to get dt
    last_time = time.time()
    pitch += gyro_x*dt
    roll += gyro_y*dt
~~~
*Note: don't actually use python's timing library to get dt. What I always do is check how fast the while loop runs in ms and set dt as a constant value*

In theory, this should be enough to tell me my orientation in space, right? Wrong! By nature, gyroscopes are nice and steady over short periods of time, but they are quite susceptible to drift (over a long period of time, you'll see the angles change even if the IMU is perfectly still). This is why we also need an accelerometer.

## Accelerometers
These are pretty straight-forward. These sensors will give you the magnitude and direction of acceleration. Thus, when the accelerometer is in steady-state, it will give us the direction and magnitude of gravity, which makes it very easy to get our orientation in space with some simple math:

$$
pitch = arctan(\frac{a_y}{\sqrt{a_x^2 + a_z^2}}) \\
roll = arctan(\frac{-a_x}{a_z})
$$

Now you're thinking "why do we need the gyroscope then?". Long story short, accelerometers tend to be more "jumpy" in the short term and there are also situations where accelerometers can't reliably tell us our position. For example, if I accelerate the system, it's no longer just picking gravity and we have lost our point of reference to find orientation.

## Enter Sensor Fusion (Complementary Filter)
Now we know two things: accelerometers are good on the long term and gyroscopes are good on the short term. These two sensors seem to **complement** each other and that's exactly why I'm going to present the complementary filter algorithm.

The core idea is that we use the gyroscope as our main underlying signal, then use a certain percentage of the accelerometer to compensate for any drift of the gyro sensor. Ultimately, we are using the strengths of both sensors to *complement* each other.

## Example with an ICM-20948
I recently got my hands on one of <a href="https://www.sparkfun.com/products/16832">these breakout boards</a>. It's a fun little board that conveniently spits out data from an ICM-20948 IMU chip over USB. This is perfect for learning how to write a complementary filter because I can easily read data in Python using the Serial library.

```python 
import time
import math
import serial
import numpy as np

GYRO_SENS = 65.536 # Each IMU has a specific sensitivity factor that you need to scale raw data into deg/s
#ACCEL_SENS = 1 # I changed some settings on my openlog board, but normally I would need a scaling factor for the accelerometer as well
pitch = 0
roll = 0
last_time = time.time()
# Connecting to the OpenLog Board via serial
ser = serial.Serial('/dev/cu.wchusbserial1420', 115200, timeout=0.1)

for i in range(1, 10000):
    # Read data over serial
    msg = ser.readline().decode("utf8").split(',')
    # Make sure the read data is correct
    if len(msg) == 14 and msg[2] != 'aX':
        aX,aY,aZ,gX,gY,gZ,mX,mY,mZ = [float(a) for a in msg[2:11]]
        accel = (aX, aY, aZ)
        gyro = (gX, gY, gZ)
        magn = (mX, mY, mZ)

        # Integrating gyroscope data
        dt = time.time() - last_time
        last_time = time.time()
        pitch += (gyro[0]/GYRO_SENS)*dt
        roll -= (gyro[1]/GYRO_SENS)*dt

        # Only use accelerometer when it's steady (magnitude is near 1g)
        forceMagnitude = math.sqrt(accel[0]**2 + accel[1]**2 + accel[2]**2)
        if forceMagnitude > 0.9 and forceMagnitude < 1.1:
            pitch = pitch*0.95 + math.atan2(accel[1], math.sqrt(accel[0]**2 + accel[2]**2) )*180/math.pi *0.05
            roll = roll*0.9 + math.atan2(-accel[0], accel[2])*180/math.pi *0.05
        
        p = (pitch*180/math.pi)
        r = (roll*180/math.pi)
        print(round(p), round(r))
```

Now that you've had the chance to try out a very simple sensor fusion algorithm, I recommend making a google search on a few other topics:
- Gimbal lock with Euler angles
- Understanding quaternions
- Kalman filter implementation

Alternatively, if all of this is giving you a headache, I would recommend checking out <a href="https://learn.adafruit.com/adafruit-bno055-absolute-orientation-sensor">this IMU breakout board</a>. It features Bosch's BNO055 IMU which includes a sensor fusion algorithm on the chip itself. Simply pull angles off the I2C bus and you'll be good to go!

