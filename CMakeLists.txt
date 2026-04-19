cmake_minimum_required(VERSION 3.28)
project(Silk.NET LANGUAGES CXX)

# ----- Project wide configuration -----

# Tell CMake where to find CMake find modules
list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_LIST_DIR}/eng/native/cmake)

# Add ExternalProject support
include(ExternalProject)

# ----- Native projects -----

add_subdirectory(./sources/OpenAL/Soft.Native)
add_subdirectory(./sources/SDL/Native)
