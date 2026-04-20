cmake_minimum_required(VERSION 3.28)
project(Silk.NET LANGUAGES CXX)

# ----- Project wide configuration -----

# Tell CMake where to find CMake find modules
list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_LIST_DIR}/eng/native/cmake)

# Add ExternalProject support
include(ExternalProject)

# ----- Native projects -----

add_subdirectory(./sources/Assimp/Native)
add_subdirectory(./sources/OpenAL/Soft.Native)
add_subdirectory(./sources/SDL/Native)
add_subdirectory(./sources/Spirv/Cross.Native)
add_subdirectory(./sources/Spirv/Reflect.Native)
add_subdirectory(./sources/Spirv/Shaderc.Native)
add_subdirectory(./sources/Spirv/Tools.Native)
add_subdirectory(./sources/Vulkan/MoltenVK.Native)
add_subdirectory(./sources/Vulkan/Vma.Native)

# Create explicit all target for native builds
add_custom_target(External.All
    DEPENDS
        External.OpenAlSoft
        External.Sdl
)
