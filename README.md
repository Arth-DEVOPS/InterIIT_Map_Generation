# Map Generation using UAV
 
 
##The problem addressed by the project-
The project addresses the problem of designing nodes for UAV sensors and platforms to develop mapping applications and observing information from top or oblique views. The UAV has been modified to produce geographically accurate ortho-rectified two-dimensional to help with topographic surveys and generate accurate maps to help out with site surveys. 

Proposed solution-
The solution utilises the PX4 repository, and the solution was designed as follows. A camera was attached to the iris quadcopter by modifying the xacro file and writing the code for the camera accessory. The node openCV_converter was designed with the purpose of capturing images at regular intervals, and OpenCV was used to execute this. Initially, the node was designed to take a snap of a single picture; however, with the help of static integers, it was repurposed for storing images with different names at regular intervals. A survey routine was then decided so as to minimise flight time while simultaneously covering the entire map. 

The takeoff and arming were controlled through a node that utilises mavros offboard control using the iris quadcopter simulated in Gazebo/SITL. PX4 has a timeout of 500ms between two Offboard commands. If this timeout is exceeded, the commander will fall back to the last mode the vehicle was in before entering offboard mode. The setpoint publishing rate thus had to be faster than 2Hz. Before entering Offboard mode, streaming the required map dependant, setpoints must already be commenced. The quad is armed and allowed to fly upon switching to the Offboard mode. The service calls are spaced out by 5 seconds such that the autopilot is not flooded with requests. We continue sending the requested pose at the appropriate rate in the same loop.

A vector was created to store the pictures,  after which all the images taken by the drone were stored into a vector in order to use the required OpenCV functions to stitch the images together, and another object was created with the purpose of storing the stitched image. When the images of different intervals are mosaicked together, they result in the formation of the map. Image stitching uses code similar to the one used in smartphones for clicking panorama photos. 

The three nodes were then included in the launch file for the quadcopter. The world location to be mapped can be modified by importing the required world file into PX4 and modifying the launch file. 

A drone makes it possible to carry out topographic surveys of the same quality as the highly accurate measurements collected by traditional methods but in a fraction of the time. This substantially reduces the cost of a site survey and specialists' workload in the field.
The maps generated are helpful in various fields such as agriculture, forestry, archaeology and architecture, environment, emergency management and traffic monitoring. The captured drone information can also be utilised as a tool for local-scale area analysis. 

Created by- Arth Banka 
Institution- Indian Institute of Technology Kanpur
 
## Dependencies
These were the dependencies used in the project.
1. cv_bridge
2. image_transport
3. roscpp
4. sensor_msgs
5. std_msgs

## Target Library
These were the target libraries used in the project.
1. OpenCV_LIBRARIES
2. catkin_LIBRARIES
