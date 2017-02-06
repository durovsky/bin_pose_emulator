cmake_minimum_required(VERSION 2.8.3)
project(bin_pose_emulator)

find_package(catkin REQUIRED
  COMPONENTS
    roscpp
    bin_pose_msgs
    tf
)

include_directories(
  ${catkin_INCLUDE_DIRS}
  ${PROJECT_SOURCE_DIR}/include/)

catkin_package(
  CATKIN_DEPENDS
    roscpp
    tf
  INCLUDE_DIRS
    include  
)

add_executable(
  ${PROJECT_NAME}
  src/main.cpp
  src/bin_pose_emulator.cpp)
target_link_libraries(
  ${PROJECT_NAME}
  ${catkin_LIBRARIES}
  yaml-cpp)
