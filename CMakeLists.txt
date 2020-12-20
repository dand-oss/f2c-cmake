cmake_minimum_required(VERSION 3.30)

project(f2c
    VERSION 1.0.0
    DESCRIPTION "Fortran-to-C translator and runtime libraries"
    LANGUAGES C
)

###############
# ASI default settings
list(APPEND CMAKE_MODULE_PATH "$ENV{ASV_CMAKE}")
include(asv_cmake_defaults)
asv_cmake_defaults( )
###############

option(BUILD_SHARED_LIB "Build shared library (DLL)." ON)

include(GNUInstallDirs)
include(CMakePackageConfigHelpers)

# Build translator and runtimes
add_subdirectory(src)
add_subdirectory(src-libs/libI77)
add_subdirectory(src-libs/libF77)

# Install top-level public header
install(FILES
    ${CMAKE_SOURCE_DIR}/f2c.h
    DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)

# Export all targets as a single f2cTargets group
install(EXPORT f2cTargets
    FILE f2cTargets.cmake
    NAMESPACE f2c::
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/f2c
)

# Generate version file
write_basic_package_version_file(
    "${CMAKE_CURRENT_BINARY_DIR}/f2cConfigVersion.cmake"
    VERSION ${PROJECT_VERSION}
    COMPATIBILITY SameMajorVersion
)

# Configure and install f2cConfig.cmake
configure_package_config_file(
    "${CMAKE_SOURCE_DIR}/f2cConfig.cmake.in"
    "${CMAKE_CURRENT_BINARY_DIR}/f2cConfig.cmake"
    INSTALL_DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/f2c
)

install(FILES
    "${CMAKE_CURRENT_BINARY_DIR}/f2cConfig.cmake"
    "${CMAKE_CURRENT_BINARY_DIR}/f2cConfigVersion.cmake"
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/f2c
)

# CPack configuration
set(CPACK_PACKAGE_NAME        "f2c")
set(CPACK_PACKAGE_VERSION     "${PROJECT_VERSION}")
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY
    "Fortran-to-C translator and runtime libraries"
)
set(CPACK_PACKAGE_VENDOR      "AppSmiths Ventures LLP")
set(CPACK_GENERATOR           "ZIP;TGZ")
include(CPack)

