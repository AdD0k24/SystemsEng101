#SystemsEng101 

#code example for a sensor to detect if the light is off and cut power from its own switch to turn off connected A/C and projector connectors

import RPi.GPIO as GPIO
# Using Raspberry Pi GPIO library is used as the sensor
import time
import os


LIGHT_SENSOR_PIN = 17
AC_RELAY_PIN = 18
PROJECTOR_RELAY_PIN = 19
SPEAKER_PIN = 20


GPIO.setmode(GPIO.BCM)
GPIO.setup(LIGHT_SENSOR_PIN, GPIO.IN)
GPIO.setup(AC_RELAY_PIN, GPIO.OUT)
GPIO.setup(PROJECTOR_RELAY_PIN, GPIO.OUT)
GPIO.setup(SPEAKER_PIN, GPIO.OUT)

def play_sound():
    os.system("aplay beep_sound.wav") 

while True:
    light_status = GPIO.input(LIGHT_SENSOR_PIN)

    if light_status == 0:  
       
        GPIO.output(AC_RELAY_PIN, GPIO.LOW)
        GPIO.output(PROJECTOR_RELAY_PIN, GPIO.LOW)
        print("Light is off. Turning off A/C and projector.")
        play_sound() 
    else:
        # Light is on, do nothing
        print("Light is on.")

    # Delay for 30 minutes before checking again
    time.sleep(1800)

# Cleanup GPIO
GPIO.cleanup()
