cmake_minimum_required(VERSION 3.15)
project(rplidar_sdk VERSION 0.1.0)

set(CMAKE_CXX_STANDARD 17)

include(CMakePackageConfigHelpers)
include(GNUInstallDirs)


add_subdirectory(src)
add_subdirectory(app)

# ==============================================================================
# Exports and remaining installation
# ==============================================================================

configure_package_config_file(cmake/config.cmake.in
        "${CMAKE_CURRENT_BINARY_DIR}/rplidar-config.cmake"
        INSTALL_DESTINATION "${CMAKE_INSTALL_DATADIR}/rplidar"
        NO_SET_AND_CHECK_MACRO)
write_basic_package_version_file(
        "${CMAKE_CURRENT_BINARY_DIR}/rplidar-config-version.cmake"
        VERSION ${rplidar_VERSION}
        COMPATIBILITY SameMajorVersion)

install(
        FILES
        "${CMAKE_CURRENT_BINARY_DIR}/rplidar-config.cmake"
        "${CMAKE_CURRENT_BINARY_DIR}/rplidar-config-version.cmake"
        DESTINATION
        "${CMAKE_INSTALL_DATADIR}/rplidar"
)

install(TARGETS rplidar EXPORT rplidar-targets)
install(DIRECTORY "include/" DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}")
install(EXPORT rplidar-targets
        NAMESPACE rplidar::
        DESTINATION "${CMAKE_INSTALL_DATADIR}/rplidar")
