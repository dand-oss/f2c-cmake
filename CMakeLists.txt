# Copyright (c) 2014 by AppSmiths Ventures LLP.  All Rights Reserved.
#
# All material is proprietary to AppSmiths Ventures LLP and may be used only
# pursuant to license rights granted by AppSmiths Ventures LLP  Other
# reproduction, distribution, or use is strictly prohibited.
#

cmake_minimum_required(VERSION 3.30)

project(
    "f2c"
    VERSION 1.0.0
    LANGUAGES C
    DESCRIPTION "netlib f2c"
    )

option(BUILD_SHARED_LIB "Build shared library (DLL)." ON)

include(GNUInstallDirs)

add_subdirectory(src)
add_subdirectory(src-libs/libI77)
add_subdirectory(src-libs/libF77)

install(FILES f2c.h DESTINATION include)

include(CPack)
