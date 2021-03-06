# Claw_Project_Max_Elias

## Table of Contents
* [Table of Contents](#TableOfContents)
* [Overview](#Overview)
* [Planning](#Planning)
* [Materials](#Materials)
* [Claw](#Claw)
* [Pulley System](#PulleySystem)
* [Final Claw](#FinalClaw)
* [Final Machine](FinalMachine)
* [Reflection](#Reflection)
---

## Overview

The goal of this project was to create a claw that can go both go up and down using a pulley system, and pick up a desired object all at the press of a button. This project also includes a cartisian arm system where the claw can move on a y and x axis. 

## Planning

[Planning Document](https://docs.google.com/document/d/1XXWAfTAQtO8pT8Eb2y5HrwGSn4y9Jn23eiQkxXuFsj8/edit?usp=sharing)

## Materials

 - Metro Express Board
 - Servo 
 - Continuous Rotation Servo
 - Pushbutton
 - Breadboard
 - Wires
 - 9V Battery Pack
 - 6V Battery Pack
 - Batteries
 - 10k Resistor 

## Claw

### Claw Wiring

<img src="https://github.com/ezell38/Claw_Project_Max_Elias/blob/main/Capture.15.PNG" alt="Claw" width="500" >

### Claw CAD 

<img src="https://github.com/ezell38/Claw_Project_Max_Elias/blob/main/Capture.12.PNG" alt="Claw" width="500" >

<img src="https://github.com/ezell38/Claw_Project_Max_Elias/blob/main/Capture.14.PNG" alt="Claw" width="500" >

<img src="https://github.com/ezell38/Claw_Project_Max_Elias/blob/main/Capture.13.PNG" alt="Claw" width="500" >

[OnShape Link](https://cvilleschools.onshape.com/documents/1f5db2379f1d2c9b7195486e/w/dd9e2ac12dc3a1b1d58a8a94/e/bb594a6de6861d6ebeffe694)

### Claw Code

```python
# Claw project Code
# Elias Zell & Max Timmins
# This code should control four servos to make a claw open and close when a button is pressed
import pwmio
import servo
import board
import digitalio
from digitalio import DigitalInOut, Direction, Pull

btn = DigitalInOut(board.D2)
btn.direction = Direction.INPUT
btn.pull = Pull.DOWN

counter = 0

pwm = pwmio.PWMOut(board.A2, duty_cycle=2 ** 15, frequency=50)
pwm1 = pwmio.PWMOut(board.A3, duty_cycle=2 ** 15, frequency=50)

my_servo1 = servo.Servo(pwm)
my_servo2 = servo.Servo(pwm)
my_servo3 = servo.Servo(pwm1)
my_servo4 = servo.Servo(pwm1)

# Code to open the claw
def closeClaw():  
    my_servo1.angle = 180
    my_servo2.angle = 180
    my_servo3.angle = 0
    my_servo4.angle = 0
    return 0
    
# Code to close the claw
def openClaw():
    my_servo1.angle = 90
    my_servo2.angle = 90
    my_servo3.angle = 100
    my_servo4.angle = 100
    return 1

clawState = closeClaw()

btndown = 0

# Tells the arduino that if the claw is open and the button is pressed to close the claw and if the claw is closed and the button is pressed to close it
while True:
    print(btn.value)
    if btn.value and (btndown == 0):
        print("BTN is down")
        btndown = 1
        if clawState == 1:
            clawState = closeClaw()
        else:
            clawState = openClaw()
    if not btn.value:
        btndown = 0
```        


## Pulley System 

### Pulley Wiring 

<img src="https://github.com/ezell38/Claw_Project_Max_Elias/blob/main/Capture.16.PNG" alt="Claw" width="500" >

### Pulley CAD

<img src="https://github.com/ezell38/Claw_Project_Max_Elias/blob/main/Capture.10.PNG" alt="Claw" width="500" >

<img src="https://github.com/ezell38/Claw_Project_Max_Elias/blob/main/Capture.11.PNG" alt="Claw" width="500" >

[OnShape Link](https://cvilleschools.onshape.com/documents/b4fa0afbfa2f079a6a085bd3/w/0d784bcc45420ac59128868b/e/0002819ede218a1c8613da6c)

### Pulley Code

```python 
# Claw project Pulley Code
# Elias Zell & Max Timmins
# This code should control a servo to make it rotate forwards and backwards when the button is pressed
import time
import board
import pwmio
from adafruit_motor import servo
from digitalio import DigitalInOut, Direction, Pull

btn = DigitalInOut(board.D2)
btn.direction = Direction.INPUT
btn.pull = Pull.DOWN

# create a PWMOut object on Pin A2.
pwm = pwmio.PWMOut(board.A2, frequency=50)

# Create a servo object, my_servo.
my_servo = servo.ContinuousServo(pwm)

lastButtonState = 0
btndown = False


while True:
# This section makes sure it only runs the code once per button press
    if btn.value and lastButtonState == 0: 
        btndown = not btndown
# This section tells the servo that if the button last rotated backwards it needs to go forwards        
        if btndown is True:  
            print("Forward")
            my_servo.throttle = 1.0
            time.sleep(2.0)
            print("Stop")
            my_servo.throttle = 0.0
            time.sleep(2.0)
# This section tells the servo that if it last rotated forwards it needs to go backwards
        else:
            print("Reverse")
            my_servo.throttle = -1.0
            time.sleep(2.0)
            print("Stop")
            my_servo.throttle = 0.0
            time.sleep(2.0)
    if not btn.value:
        lastButtonState = btn.value
        print("stop")
        my_servo.throttle = 0.0
        time.sleep(0.1)
```


## Final Claw

### Evidence 

<img src="https://github.com/ezell38/Claw_Project_Max_Elias/blob/main/ezgif-1-378827971a.gif" alt="Final" width="500" >

## Final Machine 

### CAD

<img src="https://github.com/ezell38/Claw_Project_Max_Elias/blob/main/Capture.25.PNG" alt="Final" width="500" >

<img src="https://github.com/ezell38/Claw_Project_Max_Elias/blob/main/Capture.26.PNG" alt="Final" width="500" >

<img src="https://github.com/ezell38/Claw_Project_Max_Elias/blob/main/Capture.27.PNG" alt="Final" width="500" >

<img src="https://github.com/ezell38/Claw_Project_Max_Elias/blob/main/Capture.28.PNG" alt="Final" width="500" >

[OnShape Link](https://cvilleschools.onshape.com/documents/695cba3d23d16f8f9caf6ec8/w/0d2d27f6491b0545633c9ce1/e/a5e01622689d770aeaa0df81)

### Physical Product 

<img src="https://github.com/ezell38/Claw_Project_Max_Elias/blob/main/done1.gif" alt="Final" width="500" >


## Reflection

Besides minor errors and inefficiencies in our code the only major mistake we made during this project was in the construction of our claw. In the first of two prints we made all parts on the claw to thin and did not create a way for the claw to attach to the larger machine. 

