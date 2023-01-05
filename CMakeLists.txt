cmake_minimum_required(VERSION 3.8)
project(ros2opc)

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(std_msgs REQUIRED)

add_executable(ros2opc
  src/ros2opc/ros2opc.cpp
  src/ros2opc/open62541.c
  include/ros2opc/open62541.h
)

target_include_directories(ros2opc PUBLIC 
  include/ros2opc
  /opt/ros/humble/include/**
)

ament_target_dependencies(ros2opc rclcpp std_msgs)

install(TARGETS
  ros2opc
  DESTINATION lib/${PROJECT_NAME})

ament_package()
