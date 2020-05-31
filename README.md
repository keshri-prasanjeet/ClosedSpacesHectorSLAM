# ClosedSpacesHectorSLAM
Hector SLAM optimized for closed spaces with obstacle recognition and avoidance

This repository is a modification of the widely used Hector SLAM package for ROS https://github.com/tu-darmstadt-ros-pkg/hector_slam
The original version is enough for most of the use cases but in situations when the LIDAR does not have an on-board IMU such in the case of some cheaper versions of RP-LIDARs, a suddden chnage in angle or an uneven surface can lead to the map getting fuzzy and incoherent. 
The files have been modified to also allow some degree of obstacle recognition which can be seen on terminal which runs the mapping nodes.

The details of the modifies file are as follows:

1.	In the file home/catkin__ws/src/hector_slam/hector_mapping/include/hector_slam_lib/matcher/ScanMatcher.h. Two variables H and dTr of eigen Matrix type can be used for understanding the environment and build the hector slam on top of. Out of the two, H of 3x3 size is used to make the obstacle avoidance system. After close examination out of the 9 data points, the matrix element H(2,1) was chosen. Any obstacle under 40cm range (with occasional error of 5 cms) will return a message “Too close” with the value which the element (2,1) returns on the terminal screen. The code returns this message when any obstacle returns a value greater than 140.00. (which is equal to obstacle under 40cm)

2.	In the file home/catkin__ws/src/hector_slam/hector_mapping/include/hector_slam_lib/matcher/ScanMatcher.h. Two variables H and dTr of eigen Matrix type can be used for understanding the environment and build the hector slam on top of. Out of the two, H of 3x3 size is used to make the obstacle avoidance system. After close examination out of the 9 data points, the matrix element H(2,1) was chosen. Any obstacle under 40cm range (with occasional error of 5 cms) will return a message “Too close” with the value which the element (2,1) returns on the terminal screen. The code returns this message when any obstacle returns a value greater than 140.00. (which is equal to obstacle under 40cm)

3.	In the file home/catkin__ws/src/hector_slam/hector_mapping/src/HectorMappingRos.cpp.
To change the threshold of map updation, i.e. changing the limit under which the algorithm will not update the map. To achieve this the argument variable map_update_distance_thresh can be changed from 0.4 to something larger for lesser sensitivity. Similar change is needed to be made in the file home/catkin__ws/src/hrctor_slam/hector_mapping/launch/mapping_default.launch

4.	In the file home/catkin__ws/src/hector_slam/hector_mapping/src/HectorMappingRos.cpp
and home/catkin__ws/src/hrctor_slam/hector_mapping/launch/mapping_default.launch
To change the threshold of the angle which affects the sensitivity of the map, the value of map_update_angle_thresh must be changed from 0.9 in HectorMappingRos.cpp and from 0.06 from mapping_default.launch to a larger value.

Footnotes: 
  All the developments were done in Ubuntu 18.04 LTS which supports ROS Melodic.
