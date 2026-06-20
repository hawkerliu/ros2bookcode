cmake_minimum_required(VERSION 4.2)
project(demo_cpp_pkg)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
# uncomment the following section in order to fill in
# further dependencies manually.
# find_package(<dependency> REQUIRED)

# 1.查找 rclcpp 头文件和库
find_package(rclcpp REQUIRED)
# 2. 添加可执行文件 cpp_node
add_executable(cpp_node src/cpp_node.cpp)
# 3. 为 cpp_node 添加依赖
# target_link_libraries 这个命令已经被官方弃用, 
# 官方推荐使用更现代的 CMake 方法，即直接用 target_link_libraries
target_link_libraries(cpp_node rclcpp::rclcpp)

add_executable(person_node src/person_node.cpp)
target_link_libraries(person_node rclcpp::rclcpp)


add_executable(learn_auto src/learn_auto.cpp)
target_link_libraries(learn_auto rclcpp::rclcpp)


add_executable(learn_shared_ptr src/learn_shared_ptr.cpp)
target_link_libraries(learn_shared_ptr rclcpp::rclcpp)

add_executable(learn_lambda src/learn_lambda.cpp)
target_link_libraries(learn_lambda rclcpp::rclcpp)

add_executable(learn_function src/learn_function.cpp)
target_link_libraries(learn_function rclcpp::rclcpp)
include_directories(include)
add_executable(learn_thread src/learn_thread.cpp)
target_link_libraries(learn_thread rclcpp::rclcpp)
# 4. 将 cpp_node 拷贝到 install 目录
install(TARGETS
  cpp_node
  person_node
  learn_auto
  learn_shared_ptr
  learn_lambda
  learn_function
  learn_thread
  DESTINATION lib/${PROJECT_NAME}
)


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
