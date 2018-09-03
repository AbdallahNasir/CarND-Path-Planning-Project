# Path Planning Project
This file describes how the project Path Planning was developed. 

# Files Included
The logic used is very simple, thus it was fit in a single file. For more readable code, it should have been written in classes. All variables and functions described below are written in src/main.cpp.

# Controlling variables
The main two variables in this implementation are the lane and the velocity. They are used to create the point on which the car will follow in the simulator. They are declared in line 203, 204.

If in the application is was decided to change the lane to the right, the lane variable should be increased by one. If the velocity to be increased, same should be done to the ref_vel variable. When changin the velocity, we should consider not change it too hard, to avoid high jerk.

# Sensor fusion
Sensor fusion parameter is used to monitor other cars, to make suro to avoid collisions, and decide correctly which lane to change to.

# Lanes status
Lanes status is identifed using two boolean arrays, too_close which used to tell if the cars ahead of us is very close, and safeGoLane which is used for cars behined ours. Please check lines 255 to 287.

Too close or SafeGoLane uses the location of the other car and its speed, to predict will it cross our car in the near future, adding some safety margin to make sure no collision can happen.

# Decision Making
If the next car is too close to our car in our lane, we should decide to slow down, or to swich lane. If the adjacent lane or lanes also suffers from a too close car, then there is no point of switching, thus the car will slow down. If also a car is approaching from the back in that other lane, then switching will not happen.

If in the current lane, the next car ahead of ours is far, then no decision is needed, other than speeding up to reach the speed limit.

Please check the lines from 289 to 319.

# Create the spline
The trajectory points generation is a continous job, meaning that the code will be executed always even if the car did not finish the whole trajectory. We will be calculating only new points and adding them to the points that the car will follow. Previously calculated points will not be revisited. 

A target point is set using the desired lane, and it is used to generate a Spline that will be used to control where tha car will go in a smooth way. To make the calcluations a lot more easier, we will convert the coordinates to be referred to the car instead of the map.

Please check the lines 345 to 398.

# Create the trajectory
Using the velocity and a target point, the distance between each two x values in the trajectory points will be calculated. After that, and with the initial x point, the y point for each x one will be calculated using the spline. 

The coordinates calculated using the spline will be converted back to map coordinates, and then it will be added to the trajectory for the car to follow.

Please check lines 432 to 458.
