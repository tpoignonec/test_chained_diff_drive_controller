cmake_minimum_required(VERSION 3.8)
project(test_chained_diff_drive_controller)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
endif()

install(
  DIRECTORY launch config
  DESTINATION share/test_chained_diff_drive_controller
)

ament_package()
