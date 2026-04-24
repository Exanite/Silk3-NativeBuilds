cmake_minimum_required(VERSION 3.28)
project(Silk.NET LANGUAGES CXX)

# ----- Import utilities -----

# Add ExternalProject support
include(ExternalProject)

# Add shared external project arguments
include(./eng/native/cmake/external/ExternalProjectArgs.cmake)

# ----- First-party project configuration -----

# These only apply to non-external projects since external projects are isolated
# If you want to configure all projects, modify the /eng/cmake/toolchain/GlobalOptions.cmake file

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
endif()

# ----- Define build all target -----

# This section creates an explicit all target for convenience
# For example, on Jetbrains IDEs, there is no option to build all targets, so this acts as a substitute

# Define a list of all targets
set(native_build_targets_raw
    External.Assimp
    External.MoltenVK
    External.OpenAlSoft
    External.Sdl
    External.Shaderc
    External.Shaderc
    External.SpirvCross
    External.SpirvReflect
    External.SpirvTools

    # VMA needs to be wrapped since VMA does not build as a shared library by default
    Silk.VulkanMemoryAllocator
)

# Filter out targets invalid for the current configuration
set(native_build_targets "")
foreach(target IN LISTS native_build_targets_raw)
    if(TARGET ${target})
        list(APPEND native_build_targets ${target})
    endif()
endforeach()

add_custom_target(BuildNative DEPENDS ${native_build_targets})
