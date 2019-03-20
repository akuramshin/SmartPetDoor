# SmartPetDoor
A smart pet door.

A project I made in my junior year of highschool to controll when to let my cat "Mittens" into the house. I live near a forest and my cat is an avid hunter who enjoyed to bring his catch inside the house through a wooden pet door I hand made and installed. In order to stop my cat from bringing the dead animals inside the house I decided to make a "Smart Pet Door" to manage my cats ability to enter the house.

I decided to modify our existing pet door to make it possible to controll what gets inside the house. 

- I installed a solenoid lock on one side to block entrance inside the house when the solenoid is in its passive position.
- The solenoid needed more power than the pi could supply, so a seperate power source (12V power adapter plugged into the wall) was used along side a relay to controll the solenoid (on or off).
- I installed a small PIR motion sensor pointing to the outside right beside the entrance to detect if my cat wants to go inside the house.
- I also installed a cheap webcam from dollarama pointing about at the spot where my cat would be if he wanted to get inside the house through the pet door.
- As the brains of the cat door I installed the Raspberry Pi 1 with a wifi dongle stick.

The pet door would detect movement near the entrance and instantly take a picture with the webcam. The raspberry pi would then send a GCM notification to my android phone. On my Raspberry Pi I run a local server with python, using Django, that uploads the snapshot to an index of the server. I coded a simple android app that consists of only a picture and button. The app downloads the picture from the local server through an asynchronous task to display and for me to see if "Mittens" is holding some sort of animal in his mouth. If I want to let my cat in, I simply press the button on the ui that accesses another index on my local server (using Django for python) which sends a signal using the GPIO pins to a relay to power on the solenoid for a set time period to unlock the door and let the cat inside.

The "src" folder contains the java code and manifest files for the Android Studio app code. 

Unfortunatly I no longer have the code I used on the Raspberry Pi. basically, I set up a very simple Django local server with 2 indexes, "open" and "pic.jpg". If the "open" index was accessed (the user pressing the "open" button), the Pi knew to trigger the relay with a GPIO pin. The "pic.jpg" index just displayed an image stored in the folder with the python script which would be an image the webcam takes. While the server is running, I have a threaded loop listening for a HIGH signal from the motion detector. If a signal is recieved, the Pi triggers the webcam to take a picture and save it as "pic.jpg", overwriting the old picture, and the Pi also sends a GCM message to the user's phone.
