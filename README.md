# Hairy-Product
Robot with wifi router, which tries to disconnect all the client. 
This project's functions separates into 3 phases.
1. Standby phase, which is robot waiting for devices connecting to the robot.
2. Avoidance Phase, since wifi does not have function of detecting devices' distance or direction, it has avoidance movement with Ultra Sonic Range Detector to runs around.
3. Motion Detect Phase, after 30sec of Avoidance, robot will stop and look out for motions if there's any people around it.

This project is constructed with:

1.OSEPP Basic Robot Kit 101
2.Sparkfun Wifly Shield
3.OSEPP Ultra Sonic Range Finder x2
4.OSEPP PIR Detector
5.Servo Motor
6.Photosensor

Photosensor goes on top of Wifly shield's built-in LED GPIO4 with any kind of tapes which can shuts out any lights.

Wifly Shield should be set up as AP mode, and set wifly "GPIO Alternative Function", which allows wifly to have function turning on the LED when its connected.



