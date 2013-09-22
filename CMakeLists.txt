# Copyright (C) 2013 Appzlab
# See the LICENSE file for copying permission.
#
# CMake Build System
# ------------------
#
# How to build the project:
# 
#  > mkdir build && cd build
#  > cmake ..
#  > make
# ---------------------------------------------
cmake_minimum_required(VERSION 2.8 FATAL_ERROR)

# Setup the project
project(RESTC C)

# Add find modules to the path
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/Modules/")

# Build options
option( IPV6_SUPPORT			"Enable IPv6 Support"				ON )
option( SSL_SUPPORT				"Enable SSL Support"				OFF )
option( MULTITHREAD_SUPPORT		"Enable Multithreaded Hardware"		ON )

# Configuration
set(RESTC_NAME "restc")
set(RESTC_SOURCES "src/restc.c")
set(RESTC_INCLUDES "include")
set(RESTC_LIBS "")

# Find libmicrohttpd
find_package(libmicrohttpd REQUIRED)

# Include Directories
include_directories(${RESTC_INCLUDES} ${MHD_INCLUDE_DIRS})

# Compile the code
add_executable(${RESTC_NAME} ${RESTC_SOURCES})

# Link libraries
target_link_libraries(${RESTC_NAME} ${MHD_LIBRARIES})