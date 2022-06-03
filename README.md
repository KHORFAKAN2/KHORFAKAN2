I do not know where to start writing about this topic, and I know that it is an important topic for us,
as the small opinion that I will express through this topic does not agree with this topic,
which has been talked about by many before me,
but I promise you that I will try hard to give This topic is true and I am organizing my thoughts related to this topic and adding them to you. 
I hope that this helps me. Hello my friends, I am the student Khaled, the team leader, and my colleagues Khaled the programmer and the engineer Zayed.
We are a team of future Khorfakkan engineers 1 . We cooperate in the work and distribute the work in the organization. We train weekly and organize our times. But now I will inform you about our vehicle.

In the WRO Future Engineers category teams need to focus on all parts of the engineering
process. The teams get bonus points for documenting their process and making a public
GitHub repository. The specific challenge will change every 3-4 year.
In the Self-Driving Cars challenge a robotic vehicle needs to drive autonomously on a parkours
that randomly changes each round.

How does an electric car work?

"Electric cars run on power provided by rechargeable batteries. Unlike conventional cars, electric cars use single-speed transmissions because their engine delivers maximum torque and power at extremely low speeds."

Transmission differences between conventional and electric vehicles.
Electric cars, or fully electric cars, rely entirely on electricity stored in the battery pack to move the wheels, unlike internal combustion cars that run on conventional fuels (gasoline or diesel). When a conventional car runs out of fuel, the driver has to stop at a gas station to fill up the car's tank. In return, the driver of the electric car can recharge the battery using an external source of electricity. Rechargeable hybrid cars have a gasoline or diesel engine along with an electric motor, but the driver of the car can recharge the battery in the same way.
 Because the electric motor can generate torque at very low speeds, electric cars use a single-speed transmission, unlike conventional cars that need multiple gears. Conventional engines generate their power in a narrow engine speed range, so a number of gears are required to keep the engine speed in a range that provides better engine efficiency.

Basic components of an electric car
Battery: stores the electricity needed to move the car.
 Transmission: The single-speed transmission in an electric motor transfers mechanical energy from the engine to drive the wheels.
 Charging point: Allows the vehicle to be connected to an external source of electricity for charging.
The charger on the car: converts the alternating current from the charging point into direct current to charge the battery, and also checks the battery status and charging position.
 The power electronics control system: controls the engine speed and torque in order to control the flow of electrical energy.

The codes that we used : 

1- from time import sleep
import RPi.GPIO as GPIO
GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)
    #steering motors
GPIO.setup(2, GPIO.OUT)
GPIO.setup(3, GPIO.OUT)
#driving motors
GPIO.setup(4, GPIO.OUT)
GPIO.setup(17, GPIO.OUT)
global p1
global p2
p1= GPIO.PWM(4,100)
p2= GPIO.PWM(17,100)
def move(steering=0,direction=0,time=1,speed=43):
    if steering<0:
        GPIO.output(2,0)
        GPIO.output(3,1)
    elif steering>0:
        GPIO.output(2,1)
        GPIO.output(3,0)
    else:
        GPIO.output(2,0)
        GPIO.output(3,0)
    if time!=0:    
        if direction>=0:
            GPIO.output(17,0)
            p1.start(speed)
            sleep(time)
            p1.stop()
            GPIO.output(2,0)
            GPIO.output(3,0)
        else:
            GPIO.output(4,0)
            p2.start(speed)
            sleep(time)
            p2.stop()
            GPIO.output(2,0)
            GPIO.output(3,0)
    else:
        if direction>=0:
            GPIO.output(17,0)
            p1.start(speed)
        else:
            GPIO.output(4,0)
            p2.start(speed) 
def turn(direction=0,time=1):
    if direction<0:
        GPIO.output(2,0)
        GPIO.output(3,1)
        sleep(time)
    else:
        GPIO.output(2,1)
        GPIO.output(3,0)
        sleep(time)
    GPIO.output(2,0)
    GPIO.output(3,0)
def stopAll():
    GPIO.output(2,0)
    GPIO.output(3,0)
    p1.stop()
    p2.stop()
'''
GPIO.output(2,0)
GPIO.output(3,0)
p1.stop()
p2.stop()
'''

2- import RPi.GPIO as GPIO
from time import *
GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)
trig=14
echo=15
GPIO.setup(trig,GPIO.OUT)
GPIO.setup(echo,GPIO.IN)
GPIO.output(trig,GPIO.LOW)
sleep(2)
while True:
    GPIO.output(trig,GPIO.LOW)
    start_time=time()
    while GPIO.input(echo)==1:
        print('Hi')
    bounce_time=time() 
    duration= bounce_time-start_time
    #print(duration)
    distance=round(duration*1715000,0)
    print(distance)
    sleep(0.1)
GPIO.cleanup()
    
    
    3- import cv2
import numpy as np
cap= cv2.VideoCapture(0)
cap.set(3,480)
cap.set(4,320)



while True:
    # reading frams # _ means through away variable
    
    
    _,frame= cap.read()
    ,width,= frame.shape
    
    
    
    frame=cv2.rotate(frame,cv2.ROTATE_180)
    hsv_frame=cv2.cvtColor(frame,cv2.COLOR_BGR2HSV)
    
    low_red= np.array([170,50,50])
    high_red= np.array([180,255,255])
    
    
    
    red_mask= cv2.inRange(hsv_frame, low_red, high_red)
    
    ,Rcontours,= cv2.findContours(red_mask,cv2.RETR_TREE ,cv2.CHAIN_APPROX_SIMPLE)
    Rcontours=sorted(Rcontours,key=lambda x:cv2.contourArea(x), reverse=True)
    
    #for cnt in Rcontours:
    #    (x,y,w,h) = cv2.boundingRect(cnt)
     #   cv2.rectangle(frame,(x,y),(x+w,y+h),(0,255,0),2)
     #   break
    center = 0
    for cnt in Rcontours:
        (x,y,w,h) = cv2.boundingRect(cnt)
        center= int((x+x+w)/2)
        break
    
    cv2.line(frame,(center,0),(center,320),(0,255,0),2)
    cv2.line(frame,(int(width/2),0),(int(width/2),320),(0,0,255),2)
    
    cv2.imshow("Frame",frame)
    cv2.imshow("Red Mask",red_mask)
    cv2.imshow("HSV",hsv_frame)
    key= cv2.waitKey(1)
    
    if key==27:
        break
    
cap.release()
cv2.destroyAllWindows()

Since every beginning must have an end, here I have come to the conclusion of my speech, and accordingly I believe that we must unite and strive with all our energy to provide what is good for our society; By giving such projects sufficient to ensure the development and civilized societies in the long term. We want to become the future engineers of our dear country, to develop its leadership and economy, making it the first in the world .

 Thank you for your kind cooperation with us, thank you and see you soon.

https://youtu.be/CMEEup3t-Uw
![image](https://user-images.githubusercontent.com/106826821/171911207-b7c5dfff-d5e2-4ae2-bf33-ceb3e9bd8239.png)
