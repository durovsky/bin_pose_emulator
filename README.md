# bin_pose_emulator

Generator of random bin poses. It provides a ROS Service */bin_pose* which returns a combination of 3 Poses - **Grasp Point**, **Approach Point** and **Deapproach point** from predefined Virtual Bin. The Approach point is located at the normal vector given by Grasp Point orientation and the Deapproach point is located right above the grasp point.

###Usage

```
roslaunch bin_pose_emulator bin_pose_emulator
```
call ros service with an Empty request:
```
rosservice call /bin_pose
```

Service response:
```
grasp_pose: 
  position: 
    x: 0.582990474831
    y: 0.132920391803
    z: 0.110564293991
  orientation: 
    x: 0.113430335549
    y: 0.71905280478
    z: -0.119797227723
    w: 0.675089066083
approach_pose: 
  position: 
    x: 0.589268137291
    y: 0.132782671333
    z: 0.210366960715
  orientation: 
    x: 0.113430335549
    y: 0.71905280478
    z: -0.119797227723
    w: 0.675089066083
deapproach_pose: 
  position: 
    x: 0.582990474831
    y: 0.132920391803
    z: 0.260564299952
  orientation: 
    x: 0.113430335549
    y: 0.71905280478
    z: -0.119797227723
    w: 0.675089066083
```

###Visualization

In order to simplify configuration and usage of this emulator, simple visualization is provided - **bin_pose_emulator** publishes two (*visualization_msgs/Marker*) messages to **bin_pose_visualization** topic. Use **Marker** view in RViz to see the pose of virtual bin and the location of current grasp point. Both Markers are published with *base_link* as reference frame. 

<img src="http://www.smartroboticsys.eu/wp-content/uploads/2016/12/bin_pose_emulator.jpg" width="750">

###Config

Virtual Bin is defined by **bin_center_** and **bin_size_** parameters, while allowed orientation is set by roll, pitch and yaw range. By default we assume that **tool0 link** of robot is aligned with vertical axis, pointing to the ground - RPY is [0,90,0]. **roll_range**, **pitch_range** and **yaw_range** extend this default pose orientation into allowed grasp cone. 
**Approach distance** defines how far on normal vector given by Grasp Point orientation is Approach point located. The **deapproach_height** configures height of vertical movement when moving away from Grasp Point. 

Example Yaml config file: 
```
bin_center_x: 0.5
bin_center_y: 0
bin_center_z: 0.1

bin_size_x: 0.2
bin_size_y: 0.5
bin_size_z: 0.1

roll_range: 0.707
pitch_range: 0.707
yaw_range: 0.707

approach_distance: 0.1
deapproach_height: 0.15
```

###Video
Folowing [video](https://youtu.be/l4nY1mkcvU8) demonstrates capabilities of bin_pose_emulator 
