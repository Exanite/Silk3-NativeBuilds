# Define relevant folders
set(source_dir ${CMAKE_SOURCE_DIR}/eng/submodules/spirv-reflect)
set(build_dir ${CMAKE_BINARY_DIR}/build/spirv-reflect)
set(install_dir ${CMAKE_BINARY_DIR}/install/spirv-reflect)

# Define external project
silk_get_external_project_args(external_project_args ${install_dir})
ExternalProject_Add(External.SpirvReflect
    SOURCE_DIR ${source_dir}
    BINARY_DIR ${build_dir}
    INSTALL_DIR ${install_dir}
    CMAKE_ARGS
        ${external_project_args}

        # Build shared library
        -DBUILD_SHARED_LIBS=ON
)
