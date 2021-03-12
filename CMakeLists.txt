cmake_minimum_required(VERSION 3.0.0)
project(line_sensor_plugin VERSION 0.1.0)

find_package(gazebo REQUIRED)

find_package(catkin REQUIRED COMPONENTS
  gazebo_plugins
  gazebo_ros
  roscpp
)

catkin_package(
  INCLUDE_DIRS plugins/include
  CATKIN_DEPENDS gazebo_plugins gazebo_ros roscpp
)

include_directories(${catkin_INCLUDE_DIRS}
                    ${Boost_INCLUDE_DIR}
                    ${GAZEBO_INCLUDE_DIRS}
)

link_directories(${GAZEBO_LIBRARY_DIRS})


set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${GAZEBO_CXX_FLAGS}")

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

include_directories(plugins/include)

add_library(line_sensor_plugin SHARED plugins/src/line_sensor_plugin.cpp)

target_link_libraries(line_sensor_plugin CameraPlugin ${catkin_LIBRARIES} ${GAZEBO_LIBRARIES})

