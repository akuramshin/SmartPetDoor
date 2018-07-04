# SmartPetDoor
A smart pet door.

A project I made in my junior year of highschool to controll when to let my cat "Mittens" into the house or not. I live near a forest and my cat is an avid hunter who enjoyed to bring his catch inside the house to show off through the wooden pet door we installed into a basement window. This act was not appreaciated by my mom and so I thought of the idea to make my Smart Pet Door.

I decided to modify our existing pet door to make it possible to controll what gets inside the house. 

- I installed a solenoid lock on one side to block entrance inside the house when the solenoid is in its passive position.
- The solenoid needed more power than the pi could supply, so a seperate power source (12V power adapter plugged into the wall) was used along side a relay to controll the solenoid (on or off).
- I installed a small motion detector pointing to the outside right beside the entrance to detect if my cat wants to go inside the house.
- I also installed a cheap webcam from dollarama pointing about at the spot where my cat would be if he wanted to get inside the house through the pet door.
- As the brains of the cat door I installed the Raspberry Pi 1 with a wifi dongle stick.

The pet door would detect movement near the entrance and instantly take a picture with the webcam. The raspberry pi would then send a GCM notification to my android phone. On my Raspberry Pi I run a local server with python and Django that uploads the snapshot to an index of the server. I coded a simple android app that consists of only a picture and button. The app downloads the picture from the local server through an asynchronous task to display and for me to see if "Mittens" is holding some sort of animal in his mouth. If I want to let my cat in, I simply press the button on the ui that accesses another index on my local server (using python with Django) which sends a signal using the GPIO pins to a relay to power on the solenoid for a set time period to unlock the door and let the cat inside.
