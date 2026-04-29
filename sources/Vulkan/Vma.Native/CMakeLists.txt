add_library(Silk.VulkanMemoryAllocator SHARED)
set_target_properties(Silk.VulkanMemoryAllocator
    PROPERTIES
        CXX_STANDARD 23
        OUTPUT_NAME "vma"
)

file(GLOB sources CONFIGURE_DEPENDS src/*.cpp)
target_sources(Silk.VulkanMemoryAllocator PRIVATE ${sources})

target_link_libraries(Silk.VulkanMemoryAllocator PRIVATE Imported.VulkanMemoryAllocator)
