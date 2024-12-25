cmake_minimum_required(VERSION 3.10)

project(obs-shaderfilter)

# Find the OBS development files
find_package(PkgConfig REQUIRED)
pkg_check_modules(LIBOBS REQUIRED libobs)

# Include the OBS headers
include_directories(${LIBOBS_INCLUDE_DIRS} /usr/include/obs)

# Source files
set(obs-shaderfilter_PLATFORM_SOURCES
    src/obs-shaderfilter.c
)

# Create the library
add_library(obs-shaderfilter MODULE ${obs-shaderfilter_PLATFORM_SOURCES})
target_link_libraries(obs-shaderfilter ${LIBOBS_LIBRARIES})

# Set plugin properties
set_target_properties(obs-shaderfilter PROPERTIES FOLDER "plugins")

# Install the plugin and data
install(TARGETS obs-shaderfilter DESTINATION /usr/share/obs/obs-plugins)
install(DIRECTORY data DESTINATION /usr/share/obs/obs-plugins/obs-shaderfilter)
