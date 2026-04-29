# Define relevant folders
set(source_dir ${CMAKE_SOURCE_DIR}/eng/submodules/spirv-tools)
set(build_dir ${CMAKE_BINARY_DIR}/build/spirv-tools)
set(install_dir ${CMAKE_BINARY_DIR}/install/spirv-tools)

# Define external project
silk_get_external_project_args(external_project_args ${install_dir})
ExternalProject_Add(External.SpirvTools
    SOURCE_DIR ${source_dir}
    BINARY_DIR ${build_dir}
    INSTALL_DIR ${install_dir}
    DOWNLOAD_COMMAND ""
    CMAKE_ARGS
        ${external_project_args}

        # Build shared library
        -DBUILD_SHARED_LIBS=ON

        # Unnecessary features
        -DSPIRV_SKIP_EXECUTABLES=ON
        -DSPIRV_SKIP_TESTS=ON

        # Set paths to dependencies
        -DSPIRV-Headers_SOURCE_DIR=${CMAKE_SOURCE_DIR}/eng/submodules/spirv-headers
)
