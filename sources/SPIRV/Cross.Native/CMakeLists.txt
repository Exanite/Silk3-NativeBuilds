# Define relevant folders
set(source_dir ${CMAKE_SOURCE_DIR}/eng/submodules/spirv-cross)
set(build_dir ${CMAKE_BINARY_DIR}/build/spirv-cross)
set(install_dir ${CMAKE_BINARY_DIR}/install/spirv-cross)

# Define external project
silk_get_external_project_args(external_project_args ${install_dir})
ExternalProject_Add(External.SpirvCross
    SOURCE_DIR ${source_dir}
    BINARY_DIR ${build_dir}
    INSTALL_DIR ${install_dir}
    CMAKE_ARGS
        ${external_project_args}

        # Build shared library
        -DSPIRV_CROSS_STATIC=OFF
        -DSPIRV_CROSS_SHARED=ON

        # Unnecessary features
        -DSPIRV_CROSS_CLI=OFF
        -DSPIRV_CROSS_ENABLE_TESTS=OFF
)
