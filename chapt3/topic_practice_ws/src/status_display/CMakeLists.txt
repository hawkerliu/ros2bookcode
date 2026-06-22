cmake_minimum_required(VERSION 4.2)
project(status_display)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(status_interfaces REQUIRED)

find_package(Qt5 REQUIRED COMPONENTS Widgets)

add_executable(hello_qt src/hello_qt.cpp)
target_link_libraries(hello_qt Qt5::Widgets)

add_executable(sys_status_display src/sys_status_display.cpp)
target_link_libraries(sys_status_display Qt5::Widgets) # 对于非ROS功能包使用Cmake原生指令进行链接库
# 从 ROS 2 Kilted 版本开始，ament_target_dependencies() 函数已经被官方弃用。官方推荐直接使用 CMake 标准的 target_link_libraries() 配合现代 CMake 目标
# ament_target_dependencies(sys_status_display rclcpp status_interfaces)
target_link_libraries(sys_status_display rclcpp::rclcpp status_interfaces::status_interfaces)


install(TARGETS hello_qt sys_status_display
  DESTINATION lib/${PROJECT_NAME})


if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # comment the line when a copyright and license is added to all source files
  set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # comment the line when this package is in a git repo and when
  # a copyright and license is added to all source files
  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
