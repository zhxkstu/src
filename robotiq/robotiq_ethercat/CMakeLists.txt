cmake_minimum_required(VERSION 2.8.3)
project(robotiq_ethercat)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  soem
)

catkin_package(
   INCLUDE_DIRS include
   LIBRARIES ${PROJECT_NAME}
   CATKIN_DEPENDS roscpp soem
)

include_directories(include
  ${catkin_INCLUDE_DIRS}
  ## The following work around allows SOEM headers to include other SOEM headers.
  ## SOEM headers assume all headers are installed in a flat directory structure
  ## See https://github.com/smits/soem/issues/4 for more information.
  ${soem_INCLUDE_DIRS}/soem
)

add_library(${PROJECT_NAME}
 include/${PROJECT_NAME}/ethercat_manager.h
 src/ethercat_manager.cpp
)

install(TARGETS ${PROJECT_NAME}
   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
 )

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h"
)
