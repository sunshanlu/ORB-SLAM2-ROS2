cmake_minimum_required(VERSION 3.5)
project(ORB_SLAM2)

set(CMAKE_CXX_STANDARD 14)

include_directories(include)

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(OpenCV 3.1.0 REQUIRED)

add_library(DEPEND_LIBS INTERFACE)
target_link_libraries(DEPEND_LIBS INTERFACE ${OpenCV_LIBS})

file(GLOB SOURCE_FILE src/*.cc)
add_executable(${PROJECT_NAME} ${SOURCE_FILE})
ament_target_dependencies(${PROJECT_NAME} rclcpp)
# target_link_libraries传入的是target的名字
target_link_libraries(${PROJECT_NAME} DEPEND_LIBS)
install(TARGETS ${PROJECT_NAME} DESTINATION lib/${PROJECT_NAME})

add_subdirectory(test)
ament_package()