cmake_minimum_required(VERSION 3.1)
project(complementary_filter)
list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/cmake")

find_package(catkin_simple REQUIRED)

catkin_simple()

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -O3")

find_package(OpenCV REQUIRED)
find_package(Glog REQUIRED)
find_package(gflags REQUIRED)

# make libraries
cs_add_library(${PROJECT_NAME} src/complementary_filter.cpp
							   src/bag_player.cpp
							   src/utils.cpp)

# link required libraries
target_link_libraries(${PROJECT_NAME} ${OpenCV_LIBRARIES})

# make the executable
cs_add_executable(reconstruction_node src/reconstruction_node.cpp)

# link required libraries to the executable
target_link_libraries(reconstruction_node ${PROJECT_NAME} ${GLOG_LIBRARIES} ${gflags_LIBRARIES})

cs_install()
