# tesse-ros-bridge

Provides a ROS interface to the TESSE Unity environment.

## Commands
Use the following commands when having the Unity window in focus:

- Shift+T: disable keyboard input
- w,a,s,d: control agent using forces
- x: stops motion of agent.
- r: respawns agent.
- 'left ctrl + left shift + g': enter spawn point capture mode for next respawn: press 'r' until you get to a nice location, then enter capture mode so that Unity restarts where you left. Note that in this mode, it'll capture a new point every second while moving around. You can stop capturing using 'left ctrl + left shift + g'.
- ESC: to quit game.

## Prerequisites

To use this interface, first clone then setup the `tesse` package.
```bash
git clone git@github.com:MIT-TESSE/tesse-interface.git
cd tesse-interface
python setup.py develop
```

### Setup for ROS
To use this interface in ROS, you will need to import the package in the ROS folder into your catkin workspace.

```bash
# Setup catkin workspace
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin init

# Clone repo
cd src
git clone git@github.com:MIT-TESSE/tesse-ros-bridge.git

# Install dependencies from rosinstall file using wstool
wstool init
wstool merge tesse-ros-bridge/install/tesse_ros_bridge.rosinstall
wstool update

# Compile code
catkin build

# Add workspace to bashrc.
echo 'source ~/catkin_ws/devel/setup.bash' >> ~/.bashrc

# Refresh environment
source ~/.bashrc
```

## Usage

To run the ROS node:
```bash
roslaunch tesse_ros_bridge tesse_bridge.launch
```


### Plotting

You can use rviz for general visualization, we provide a configuration file:
```bash
rviz -r ./rviz/tesse_semantic_mesh.rviz
```

You can also plot IMU and ground-truth odometry from the simulator using `rqt_multiplot` and the config file we provide:
```bash
rqt_multiplot --multiplot-config:=rqt_multiplot/tesse.xml
```
