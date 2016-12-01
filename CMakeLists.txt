cmake_minimum_required(VERSION 2.8.3)
project(bin_pose_emulator)

find_package(catkin REQUIRED
  COMPONENTS
    message_generation
    roscpp
    std_msgs
    geometry_msgs
    tf
)

include_directories(
  ${catkin_INCLUDE_DIRS}
  ${PROJECT_SOURCE_DIR}/include/)

add_service_files(
  FILES
    bin_pose.srv
)

generate_messages(
  DEPENDENCIES
    std_msgs
    geometry_msgs
)

catkin_package(
  CATKIN_DEPENDS
    message_runtime
    roscpp
    std_msgs
    geometry_msgs
    tf
  INCLUDE_DIRS
    include
  LIBRARIES
    ${PROJECT_NAME}
)

# Bin pose emulator
add_executable(
  ${PROJECT_NAME}
  src/main.cpp
  src/bin_pose_emulator.cpp)
target_link_libraries(
  ${PROJECT_NAME}
  ${catkin_LIBRARIES}
  yaml-cpp)
