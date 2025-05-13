cmake_minimum_required(VERSION 3.14)
project(entropy VERSION 0.5.5 LANGUAGES CXX)

# -----------------------------------------------------------------------------
# 1) Create the header‐only INTERFACE library
# -----------------------------------------------------------------------------
add_library(entropy INTERFACE)

# Allow users to link via `entropy::entropy`
add_library(entropy::entropy ALIAS entropy)

# -----------------------------------------------------------------------------
# 2) Public include path
# -----------------------------------------------------------------------------
# This makes <entropy/enu_converter.h> etc. resolve to include/entropy/...
target_include_directories(entropy
  INTERFACE
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

# -----------------------------------------------------------------------------
# 3) Installation & Export for find_package()
# -----------------------------------------------------------------------------
include(GNUInstallDirs)

# 3a) Install headers
install(DIRECTORY include/ DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

# 3b) Install and export the INTERFACE target
install(TARGETS entropy EXPORT concordTargets)

# 3c) Install the export file so that `find_package(entropy)` works
install(EXPORT concordTargets
  FILE concordTargets.cmake
  NAMESPACE entropy::
  DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/entropy
)

# 3d) Also export it for in‐source FetchContent usage
export(EXPORT concordTargets
  FILE "${CMAKE_CURRENT_BINARY_DIR}/concordTargets.cmake"
  NAMESPACE entropy::
)

