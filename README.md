# Tello EDU Security Drone Research // Musser Undergrad Research

This repo includes all the code I have written over the semester for research with the Tello EDU drone.
I have attepted to create a security-type system, that scans the perimeter of a household. My first idea
was to use Tello indoors to follow a security route through the house and check the windows, but I noticed 
very quickly the drone was very loud for this kind of purpose, and wouldnt be very applicable as a solution.

Due to the short battery life of the drone, I decided it would have to make an efficeint perimeter. I used
the mission control pads to create the perimeter so the drone had a path to stay relative too. Even keeping
the security route short and efficient, the drone battery only lasts 1 to 2 routes. A solution to this issue 
is to have multiple drones that can switch out throughout the day. There would either have to be a fast charger 
that could charge the drone without plugging them in, or someone would have to switch out the batteries during
the session, which sort of defeats the purpose. Maybe Ryze has another drone in development that would be able to 
land on a wireless charger to charge the drone battery quickly and automatically so it could get back to its 
task in a timely fashion. Professor Musser mentioned a drone in development that is longer vertically that lands
in a charging socket. This is the kind of drone that would be better suited for this task.

Most of the code to setup the connection over UDP and begin sending commands to drone is already written for python.
I used this code from https://tello.oneoffcoder.com/python-auto-flight.html in order to initialize the Tello to 
connect to my PC over UDP. All of the commands and video stream communication is my own work. I didnt see the sense 
in remaking the wheel to set up the connection, and instead spent time on creating the security path feature.

In order for the Tello video stream to be allowed through Windows Firewall, you must follow this guide to set up
and inbound rule for UDP port 11111 that the Tello sends video stream over. 

Inbound Rule Guide: https://www.mathworks.com/help/supportpkg/ryzeio/ug/enabling-video-receive-udp-port.html

