# TurtleBot3-simulation-in-ROS-Noetic
This project demonstrates how to install and use the TurtleBot3 simulation in ROS Noetic, create a map using gmapping, and then use the map for navigation.

### Steps to Set Up and Run the TurtleBot3 Simulation

#### 1. Install Necessary Packages
Update the package list and install the necessary ROS packages for TurtleBot3 and gmapping:

```bash
sudo apt-get update
sudo apt-get install ros-noetic-turtlebot3 ros-noetic-turtlebot3-msgs ros-noetic-turtlebot3-simulations
sudo apt-get install git
sudo apt-get install ros-noetic-slam-gmapping
```

#### 2. Clone TurtleBot3 Simulations Repository
Clone the TurtleBot3 simulations repository from GitHub:

```bash
git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
```

#### 3. Set Up Environment Variables
Set the TurtleBot3 model environment variable to "burger" and source the `.bashrc` file:

```bash
echo "export TURTLEBOT3_MODEL=burger" >> ~/.bashrc
source ~/.bashrc
```

#### 4. Build the Workspace
Navigate to your catkin workspace, build it, and source the setup file:

```bash
cd ~/catkin_ws
catkin_make
source devel/setup.bash
```

#### 5. Launch the TurtleBot3 Simulation
Start the TurtleBot3 Gazebo simulation with an empty world:

```bash
roslaunch turtlebot3_gazebo turtlebot3_empty_world.launch
```
![Turtlesim running](https://github.com/reham-ali102/TurtleBot3-simulation-in-ROS-Noetic/blob/main/1.jpg)

#### 6. Start Teleoperation to Move the Robot
In a new terminal, start the teleoperation node to control the TurtleBot3:

```bash
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```

#### 7. Launch Gmapping for SLAM
In another terminal, launch the gmapping demo for SLAM:

```bash
roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping
```
![Turtlesim running](https://github.com/reham-ali102/TurtleBot3-simulation-in-ROS-Noetic/blob/main/2.jpg)

#### 8. Save the Map Once Created
Once you have moved the robot around enough to create a complete map, save the map using the `map_saver` node:

```bash
rosrun map_server map_saver -f ~/map
```

This will save the map files (`map.pgm` and `map.yaml`) in your home directory.

#### 9. Use the Saved Map for Navigation
Launch the navigation node with the map you saved:

```bash
roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map.yaml
```

#### 10. Visualize and Set Navigation Goals in RViz
Open RViz to visualize the robot and the map, and set navigation goals:

```bash
roslaunch turtlebot3_navigation turtlebot3_navigation_rviz.launch
```
