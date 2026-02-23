cmake_minimum_required(VERSION 3.8)
project(ros2_launch_demo)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# Find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)

# Build Talker
add_executable(talker src/talker.cpp)
ament_target_dependencies(talker rclcpp)

# Build Listener
add_executable(listener src/listener.cpp)
ament_target_dependencies(listener rclcpp)

# Install Executables
install(TARGETS
  talker
  listener
  DESTINATION lib/${PROJECT_NAME}
)

# CRITICAL STEP: Install the launch files
install(DIRECTORY launch
  DESTINATION share/${PROJECT_NAME}
)

ament_package()