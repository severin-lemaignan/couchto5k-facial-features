cmake_minimum_required(VERSION 2.8.3)
project(facialexpression)

set(CPACK_PACKAGE_VERSION_MAJOR "1")
set(CPACK_PACKAGE_VERSION_MINOR "0")
set(CPACK_PACKAGE_VERSION_PATCH "0")
set(VERSION ${CPACK_PACKAGE_VERSION_MAJOR}.${CPACK_PACKAGE_VERSION_MINOR}.${CPACK_PACKAGE_VERSION_PATCH})

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/modules/")

add_definitions(-std=c++11)


find_package( TBB REQUIRED )
find_package(OpenFace REQUIRED)
include_directories(${OpenFace_INCLUDE_DIRS})

find_package(catkin REQUIRED COMPONENTS 
    roscpp 
    std_msgs
    )

catkin_package(
        INCLUDE_DIRS src
    )

include_directories(${catkin_INCLUDE_DIRS})

add_executable(facialexpression_node src/FeatureExtraction.cpp)
target_link_libraries(facialexpression_node ${catkin_LIBRARIES} ${OpenFace_LIBRARIES})

install(TARGETS facialexpression_node 
        RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})

