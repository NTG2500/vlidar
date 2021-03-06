#==============================================================================
# Copyright (c) 2011 Pavel Kartavyy <p.kartaviy@gmail.com>
#==============================================================================
CMAKE_MINIMUM_REQUIRED(VERSION 2.6.0)

PROJECT(VLIDAR)

MESSAGE(STATUS "Creating vlidar")

IF(NOT CMAKE_BUILD_TYPE)
    SET(CMAKE_BUILD_TYPE DEBUG)
ENDIF(NOT CMAKE_BUILD_TYPE)

# build libraries type
IF(NOT BUILD_SHARED_LIBS)
    SET(BUILD_SHARED_LIBS ON)
ENDIF(NOT BUILD_SHARED_LIBS)

# build directory config
SET(LIBRARY_OUTPUT_PATH ${CMAKE_CURRENT_BINARY_DIR})
SET(EXECUTABLE_OUTPUT_PATH ${CMAKE_CURRENT_BINARY_DIR})

# work with cmake
SET(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)

#warning level
SET(CMAKE_CXX_WARNING_LEVEL 4)

INCLUDE(FindOS)

FIND_PACKAGE(QWT REQUIRED)
LINK_DIRECTORIES(${QWT_LIBRARIES})
INCLUDE_DIRECTORIES(${QWT_INCLUDE_DIR})

FIND_PACKAGE(URG REQUIRED)
LINK_DIRECTORIES(${URG_LIBRARIES})
INCLUDE_DIRECTORIES(${URG_INCLUDE_DIR})

#FIND_PACKAGE(OpenCV)
#LINK_DIRECTORIES(${OpenCV_LINK_DIRECTORIES})
#INCLUDE_DIRECTORIES(${OpenCV_INCLUDE_DIR})

FIND_PACKAGE(Qt4 COMPONENTS QtGui QtCore REQUIRED)
INCLUDE(${QT_USE_FILE})

# add the include folder to the include path
INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR})

SET(VLIDAR_SOURCE_DIR ${PROJECT_SOURCE_DIR}/vlidar)
ADD_SUBDIRECTORY(${VLIDAR_SOURCE_DIR})

SET(CDEFS "-DLIDAR")

SET(CMAKE_C_FLAGS  ${CDEFS})
SET(CMAKE_CXX_FLAGS ${CDEFS})

