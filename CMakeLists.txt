# Copyright (c) 2014 by AppSmiths Ventures LLP.  All Rights Reserved.
#
# All material is proprietary to AppSmiths Ventures LLP and may be used only
# pursuant to license rights granted by AppSmiths Ventures LLP  Other
# reproduction, distribution, or use is strictly prohibited.
#

cmake_minimum_required(VERSION 3.1)

project(f2c C)

###############
# ASI default settings
list(APPEND CMAKE_MODULE_PATH "$ENV{ASV_CMAKE}")
include(asv_cmake_defaults)
asv_cmake_defaults( )
###############

add_subdirectory(src)
add_subdirectory(src-libs/libI77)
add_subdirectory(src-libs/libF77)

install(FILES f2c.h DESTINATION include)
