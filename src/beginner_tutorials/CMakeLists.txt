
cmake_minimum_required(VERSION 2.8.3)
project(beginner_tutorials)

## Find catkin and any catkin packages
find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  actionlib_msgs
  cv_bridge
  image_transport
  message_generation
)

add_message_files(
    FILES
    IoTSensor.msg
    )

add_service_files(
  FILES
  AddTwoInts.srv
  )

add_action_files(
  DIRECTORY action
  FILES Fibonacci.action
)

## Generate added messages and services with any dependencies listed here
generate_messages(
    DEPENDENCIES 
    std_msgs 
    actionlib_msgs
    )

## Declare a catkin package
catkin_package(
  INCLUDE_DIRS include
  LIBRARIES beginner_tutorials
  CATKIN_DEPENDS roscpp rospy std_msgs message_runtime
  DEPENDS system_lib
)

## Build talker and listener
include_directories(include ${catkin_INCLUDE_DIRS})

add_executable(talker src/talker.cpp)
target_link_libraries(talker ${catkin_LIBRARIES})
add_dependencies(talker beginner_tutorials_generate_messages_cpp)

add_executable(listener src/listener.cpp)
target_link_libraries(listener ${catkin_LIBRARIES})
add_dependencies(listener beginner_tutorials_generate_messages_cpp)

add_executable(service_server src/service_server.cpp)
target_link_libraries(service_server ${catkin_LIBRARIES})
add_dependencies(service_server beginner_tutorials_generate_messages_cpp)

add_executable(service_client src/service_client.cpp)
target_link_libraries(service_client ${catkin_LIBRARIES})
add_dependencies(service_client beginner_tutorials_generate_messages_cpp)





