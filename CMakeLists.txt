cmake_minimum_required(VERSION 3.28)
project(Silk.NET LANGUAGES CXX)

# ----- Import utilities -----

# Add ExternalProject support
include(ExternalProject)

# Add shared external project arguments
include(./eng/native/cmake/external/ExternalProjectArgs.cmake)

# ----- Project wide configuration -----

# Default to release builds
if(NOT DEFINED CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif()

# ----- Native projects -----

# Most of these builds are defined as external project targets
#
# External projects are built in isolation
# This means that their variables and targets are isolated from ours
# Very few variables (usually compiler related) are automatically passed to the external project build

add_subdirectory(./sources/Assimp/Native)
add_subdirectory(./sources/OpenAL/Soft.Native)
add_subdirectory(./sources/SDL/Native)
add_subdirectory(./sources/SPIRV/Cross.Native)
add_subdirectory(./sources/SPIRV/Reflect.Native)
add_subdirectory(./sources/SPIRV/Shaderc.Native)
add_subdirectory(./sources/SPIRV/Tools.Native)
add_subdirectory(./sources/Vulkan/Native)
add_subdirectory(./sources/Vulkan/Vma.Native)
add_subdirectory(./sources/Vulkan/Vma.Native/External)

if(APPLE)
    add_subdirectory(./sources/Vulkan/MoltenVK.Native)
else()
    add_custom_target(External.MoltenVK)
endif()

# Create explicit all target for native builds for convenience
add_custom_target(AllTargets
    DEPENDS
        External.Assimp
        External.MoltenVK
        External.OpenAlSoft
        External.Sdl
        External.Shaderc
        External.Shaderc
        External.SpirvCross
        External.SpirvReflect
        External.SpirvTools

        Silk.VulkanMemoryAllocator
)
