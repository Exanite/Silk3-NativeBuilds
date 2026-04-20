cmake_minimum_required(VERSION 3.28)
project(Silk.NET LANGUAGES CXX)

# ----- Project wide configuration -----

# Add ExternalProject support
include(ExternalProject)

# Add shared external project arguments
include(./eng/native/cmake/ExternalProjectArgs.cmake)

# ----- Native projects -----

add_subdirectory(./sources/Assimp/Native)
add_subdirectory(./sources/OpenAL/Soft.Native)
add_subdirectory(./sources/SDL/Native)
add_subdirectory(./sources/SPIRV/Cross.Native)
add_subdirectory(./sources/SPIRV/Reflect.Native)
add_subdirectory(./sources/SPIRV/Shaderc.Native)
add_subdirectory(./sources/SPIRV/Tools.Native)
add_subdirectory(./sources/Vulkan/MoltenVK.Native)
add_subdirectory(./sources/Vulkan/Vma.Native)

# Create explicit all target for native builds
add_custom_target(External.All
    DEPENDS
        External.OpenAlSoft
        External.Sdl
)
