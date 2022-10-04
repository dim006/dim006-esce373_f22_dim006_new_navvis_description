# How to use the package to view the robot and sensor data from ROS bag files in RVIZ
+  source /opt/ros/noetic/setup.bash
+  cd catkin_make
+  catkin_make
+  source devel/setup.bash
+  cd src
+  cd new_navvis_description
+  cd launch
+  roslaunch new_display.launch &

# Launch Files
+  display.launch - has the option to load between a .urdf or .xacro file. Contains the description information of the build parameters for the robot model in rviz using the /robot_description parameter. 
<arg name="use_xacro" default="false" />
<arg name="use_gui" default="true" />
<arg if="$(arg use_xacro)" name="filename" default="navvis1.xacro" />
<arg unless="$(arg use_xacro)" name="filename" default="navvis1.urdf" />
<arg name="file" default="$(find navvis_description)/urdf/$(arg filename)" />
<arg name="use_robot_state_publisher" default="true" />

+ new_pre_display.launch - connects a new ROS package that depends on the ROS package trought its display.launch. This new XACRO file creates additional elements of the platform and joins them to the description from the display.launch
<arg name="use_xacro" value="true" />
<arg name="file" value="$(find new_navvis_description)/urdf/new_navvis.xacro" />
<arg name="use_gui" value="true" />
<arg name="use_robot_state_publisher" value="true" />

+ new_display.launch - contains same functionality of new_pre.siplay.launch but with the included arguments necessary to start the ROS bag files and the map configuration. Also, includes transformation for the wheels.
<arg name="bag_path" default="$(find new_navvis_description)/bag_files/glennan_5_complete.bag" />
<arg name="bag_args" default="/tf_trajectory:=/tf --clock" />
<arg name="map_config_path" default="$(find maps_glennan)/maps/glennan5_map.yaml" />




