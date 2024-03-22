cmake_minimum_required(VERSION 3.8)
project(pub_sub)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
# uncomment the following section in order to fill in
# further dependencies manually.
# find_package(<dependency> REQUIRED)

# add executables
add_executable(publisher_node src/publisher.cpp)
add_executable(subscriber_node src/subscriber.cpp)

# dependancies
ament_target_dependencies(publisher_node
  rclcpp
  std_msgs
)
ament_target_dependencies(subscriber_node
  rclcpp
  std_msgs
)

# Install executable
install(TARGETS
  publisher_node
  subscriber_node
  DESTINATION lib/${PROJECT_NAME})

# Install launch file
install(DIRECTORY
  launch
  DESTINATION share/${PROJECT_NAME})

# package.xml
install(FILES package.xml DESTINATION share/${PROJECT_NAME})

ament_package()
