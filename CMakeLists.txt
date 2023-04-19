cmake_minimum_required(VERSION 3.0.2)
project(first_project)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  message_generation
  tf
  nav_msgs
)

## Generate messages in the 'msg' folder
 add_message_files(
   FILES
   Odom.msg
 )

## Generate services in the 'srv' folder
 add_service_files(
   FILES
   Reset.srv
 )

## Generate actions in the 'action' folder
# add_action_files(
#   FILES
#   Action1.action
#   Action2.action
# )

## Generate added messages and services with any dependencies listed here
 generate_messages(
   DEPENDENCIES
   std_msgs
   nav_msgs
   geometry_msgs
 )

## Generate dynamic reconfigure parameters in the 'cfg' folder
# generate_dynamic_reconfigure_options(
#   cfg/DynReconf1.cfg
#   cfg/DynReconf2.cfg
# )

catkin_package(
  CATKIN_DEPENDS 
  roscpp 
  rospy 
  std_msgs 
  message_runtime
  geometry_msgs
)

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)


add_executable(odom_node src/odom_node.cpp)
add_dependencies(odom_node first_project_generate_messages_cpp)
add_dependencies(odom_node ${${first_project}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(odom_node ${catkin_LIBRARIES})
