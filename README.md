# Proustite DeltaX
Omni wheeled, ball collecting, football robot for the DeltaX 2026 competition.

The robot originally had a red and black theme, thus the name.
But I ran out of red filament and some testing pieces didn't get reprinted in black.

The competition [DeltaX 2026](https://delta.ut.ee/et/deltaX) took place 17 January 2026.

My robot ended up winning the advnaced robot football category.

## Description
Proustite is an 3 motor omni wheel ball collecting robot.

The brains of the robot is a Raspberry Pi 5 running custom Python code.

The Pi is connected to a webcam, a Nucleo and an ESP32 or Arduino.
The Nucleo is in charge of the motors and the ESP32 controls the drome motor ESC and a MPU6050 IMU sensor.

The Nucleo G431KB is running custom PID controller C++ code.
The ESP32 which broke during the competition is connected to the MPU6050 IMU sensor via I2C and to the BLHeli-S ESC via PWM.

The Nucleo and ESP32 take commands from the Pi via serial over USB.

<img width="2396" height="1340" alt="image" src="https://github.com/user-attachments/assets/0939ac1e-0161-485d-ab49-e4b6a1c08ac3" />


The robot makes the drone motor with a TPU roller start spinning slowly.
It then finds balls with its webcam and collects the balls.

After it has enough balls, it goes and deposits them into a goal which it also finds using the camera feed.

The initial plan was to find the balls with a custom trained YOLOv11 model, but the wireless was so bad at the event that the plan never got put into action.

## Design
<img width="2800" height="1630" alt="Render" src="https://github.com/user-attachments/assets/18300691-1cf5-409e-9c9d-e664f07928ee" />

The robot is mostly 3D printed out of PETG.

It is powered by a Makita 18V battery and a step-down converter. 
A 5 Ah battery lasted me the whole 7 hours. 
The step-down converter is a Chinese MT18APS available on Aliexpress.

The Raspberry Pi was powered from a Chinese Mini560 step-down, but I fried it, so I decided to use the 12V cigarette adapter that came with the MT18APS and added a USB-PD car adapter.

The car adapter couldn't meet the RPi 5 new 5V 5A power requirements, so when the motors and drone motor got connected, the USB power draw was too much for the Pi and it shut down.
Other than that it worked well.

I wouldn't use a drone motor again. The ESC was a pain as I couldn't for the life of me configure it to be reversible.
I managed to flash ESP32-FC on a spare ESP32 which acted as a drone flight controller so I could pass the ESC to a computer.

The drone motor also had a wonderful feature - it is a drone motor. 
When the ESP32 got disconnected the wrong way, the drone motor decided to flex its 20 000 RPM muscle and destroyed some stuff a couple of times.
Also when the motor stalled, the ESC reset itself and forgot all the PWM calibration, which made the roller stuck with the balls still inside.

I would recommend a simple DC motor with enough torque to grab balls and a H-bridge to control it.

I have added the STEP file too. Have fun with it.

## Competition
If I could, I would tell myself in the past to bring a reliable wireless connection.

I used my iPhone as a WiFi hotspot, but the wireless traffic was so overwhelming for my whimpy phone WiFi chipset, that my laptop had trouble connecting to the RPi.

There were many instances where I couldn't issue the needed shutdown command becuase the command just didn't reach the Pi.

I couldn't even upload working code and my robot was almost like it was waiting for a bus, just standing on the field, not moving.

The tournament was a Swiss-style tournament with a final round.

I managed to get to the final round and where I came, I saw, I conquered. 
The only win for my opponent was when I accidentally scored into my own goal because the start command I inputted was wrong and I couldn't stop my robot because of the lag.

---
This was such an awesome project. 
I really liked competing and the victory on top of that was so so sweet.

I would do this again if I could. 100%.

I hope that this repository can help someone make an even cooler robot that will dominate its field. 
