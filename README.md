# Tello EDU Security Drone Research // Musser Undergrad Research

This repo includes all the code I have written over the semester for research with the Tello EDU drone. I have attepted to create a security-type system, that scans the perimeter of a household. My first idea was to use Tello indoors to follow a security route through the house and check the windows, but I noticed very quickly the drone was very loud for this kind of purpose, and wouldnt be very applicable as a solution.

Due to the short battery life of the drone, I decided it would have to make an efficeint perimeter. I used the mission control pads to create the perimeter so the drone had a path to stay relative too. Even keeping the security route short and efficient, the drone battery only lasts 1 to 2 routes. A solution to this issue is to have multiple drones that can switch out throughout the day. There would either have to be a fast charger that could charge the drone without plugging them in, or someone would have to switch out the batteries during the session, which sort of defeats the purpose. Maybe Ryze has another drone in development that would be able to land on a wireless charger to charge the drone battery quickly and automatically so it could get back to its task in a timely fashion. Professor Musser mentioned a drone in development that is longer vertically that lands in a charging socket. This is the kind of drone that would be better suited for this task.

Most of the code to setup the connection over UDP and begin sending commands to drone is already written for python. I used this code from https://tello.oneoffcoder.com/python-auto-flight.html in order to initialize the Tello to connect to my PC over UDP. All of the commands to the drone and the connection between the video and commands of being sent using python is my own work. I didnt see the sense in remaking the wheel to set up the connection, and instead spent time on creating the security path feature.

In order for the Tello video stream to be allowed through Windows Firewall, you must follow this guide to set up and inbound rule for UDP port 11111 that the Tello sends video stream over. 

Inbound Rule Guide: https://www.mathworks.com/help/supportpkg/ryzeio/ug/enabling-video-receive-udp-port.html

Now that the video stream is allowed through the firwall, the video stream is able to come through. Using a git repository implementation that uses Node.js and FFMpeg to set up a local web server, the video stream is viewable from a browser link.

Node.js and FFMpeg video stream implementation: https://github.com/dbaldwin/tello-video-nodejs-websockets
Local browser address to view video stream: http://localhost:3000/index.html

To be clear, the python scripts actually send the commands to the drone over the 8889 Port, and the Node.js and FFMpeg implementation only recieves the UDP stream coming from the Drone over UDP port 11111, decodes it, and displays in a video feed in the browser. The low latency of the Node.js implementation is desireable. Plus being able to send the automatic script using python, and then having the video stream coming in through a browser link makes for a highly efficient implementation of a security system. This means faster startup and high efficiency video feed.

# Operation
Once the proper dependencies are installed (python 3, node.js, and FFMpeg) I was able to run the security route by first running "node index.js" at the command line while in the "tello-video-nodejs-websockets" folder. In another command line, you must run "python run.py -f SecurePerimeter.txt" while in the folder containing that python and text file. This will start the stream and the route.

# Notes
1. When running npm install when in the tello-video-receive-udp-port folder, the command line resonds with error: "npm WARN tello-video-nodejs-websockets@1.0.0 No repository field." This error can be ignored as long as its followed by: "added 1 package from 1 contributor and audited 1 package in 0.456s found 0 vulnerabilities"
2. You do not need to install the Chocolatey or Visual Studio dependencies when installing Node.js, it failed for me and everything still ran perfectly.
3. These notes are to inform you on some things I learned when creating this security feed implementation. All guides in this read me should be followed for what operating system you are using. The notes I have made could specifically be for Windows OS only.

# References
1. https://www.ryzerobotics.com/tello-edu/downloads
2. https://www.65drones.com/pages/tello-operation-guide
3. https://tello.oneoffcoder.com/python-auto-flight.html
4. https://github.com/dbaldwin/tello-video-nodejs-websockets
5. https://www.mathworks.com/help/supportpkg/ryzeio/ug/enabling-video-receive-udp-port.html
