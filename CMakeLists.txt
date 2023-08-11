cmake_minimum_required(VERSION 3.25 FATAL_ERROR)

project(viam-gstreamer
  VERSION 0.0.0
  DESCRIPTION "GStreamer library integrating with the Viam C++ SDK"
  LANGUAGES CXX
)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED True)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Everything needs threads, and prefer -pthread if available
set(THREADS_PREFER_PTHREAD_FLAG ON)
find_package(Threads REQUIRED)

find_package(viam-cpp-sdk CONFIG REQUIRED viamsdk)

add_executable(gstream-viam-module
  ${PROJECT_SOURCE_DIR}/src/viam_gstream_module/module_main.cpp)

# Require pkg-config for discovering gstreamer requirements.
find_package(PkgConfig REQUIRED)
pkg_check_modules(GSTLIBS REQUIRED
        gstreamer-1.0
)

target_include_directories(gstream-viam-module PRIVATE
  ${GSTLIBS_INCLUDE_DIRS}
)

target_link_libraries(gstream-viam-module
  viam-cpp-sdk::viamsdk
  ${GSTLIBS_LIBRARIES}
)
