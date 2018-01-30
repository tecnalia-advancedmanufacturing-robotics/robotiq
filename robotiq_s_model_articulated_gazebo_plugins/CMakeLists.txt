cmake_minimum_required(VERSION 3.1)
project(robotiq_s_model_articulated_gazebo_plugins)

find_package(catkin REQUIRED COMPONENTS std_msgs gazebo_plugins actionlib tf image_transport control_msgs trajectory_msgs geometry_msgs sensor_msgs roscpp gazebo_ros robotiq_s_model_articulated_msgs)

find_package(gazebo REQUIRED)

set(CMAKE_CXX_STANDARD 11)

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
  ${GAZEBO_INCLUDE_DIRS}
)

link_directories(
  ${GAZEBO_LIBRARY_DIRS}
)

catkin_package(
   DEPENDS gazebo_plugins gazebo_ros robotiq_s_model_articulated_msgs roscpp
)

add_library(RobotiqHandPlugin src/RobotiqHandPlugin.cpp)
target_link_libraries(RobotiqHandPlugin ${catkin_LIBRARIES})
add_dependencies(RobotiqHandPlugin ${robotiq_s_model_articulated_msgs_EXPORTED_TARGETS})

install(TARGETS RobotiqHandPlugin DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}/${PROJECT_NAME}/plugins/)

