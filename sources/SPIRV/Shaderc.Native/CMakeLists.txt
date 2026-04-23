# Define relevant folders
set(source_dir ${CMAKE_SOURCE_DIR}/eng/submodules/shaderc)
set(build_dir ${CMAKE_BINARY_DIR}/build/shaderc)
set(install_dir ${CMAKE_BINARY_DIR}/install/shaderc)

# Define external project
silk_get_external_project_args(external_project_args ${install_dir})
ExternalProject_Add(External.Shaderc
    SOURCE_DIR ${source_dir}
    BINARY_DIR ${build_dir}
    INSTALL_DIR ${install_dir}
    CMAKE_ARGS
        ${external_project_args}

        # Build shared library
        -DBUILD_SHARED_LIBS=ON
)
