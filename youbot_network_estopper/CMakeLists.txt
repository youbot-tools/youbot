cmake_minimum_required(VERSION 2.8.3)
project(youbot_network_estopper)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
########### ROS ###########
find_package(catkin REQUIRED COMPONENTS rosconsole roscpp geometry_msgs)
find_package(Boost REQUIRED COMPONENTS thread date_time filesystem system regex)

###################################################
## Declare things to be passed to other projects ##
###################################################

## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need
catkin_package(
#  INCLUDE_DIRS include
# LIBRARIES YouBotDriver soem
  CATKIN_DEPENDS rosconsole
)

###########
## Build ##
###########

## Specify additional locations of header files
include_directories(
#  include
  /usr/local/include
  ${catkin_INCLUDE_DIRS}
  ${Boost_INCLUDE_DIRS}
)

link_directories(
  /usr/local/lib
  ${catkin_LIBRARY_DIRS}
)

add_definitions(-DUSE_ROS_LOGGING)
set(CMAKE_BUILD_TYPE Release)

#copy header files
#install(DIRECTORY include/
#  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
#  FILES_MATCHING PATTERN "*.hpp" PATTERN "*.h"
#)

add_executable(heartbeat_generator src/HeartbeatGenerator.cpp)
target_link_libraries(heartbeat_generator ${catkin_LIBRARIES} serial)
