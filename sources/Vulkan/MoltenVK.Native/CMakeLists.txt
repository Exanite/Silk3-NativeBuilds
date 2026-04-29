# Define relevant folders
set(source_dir ${CMAKE_SOURCE_DIR}/eng/submodules/moltenvk)
set(build_dir ${CMAKE_BINARY_DIR}/build/moltenvk)
set(install_dir ${CMAKE_BINARY_DIR}/install/moltenvk)

# Define external project
silk_get_external_project_args(external_project_args ${install_dir})
ExternalProject_Add(External.MoltenVK
    SOURCE_DIR ${source_dir}
    BINARY_DIR ${build_dir}
    INSTALL_DIR ${install_dir}
    DOWNLOAD_COMMAND ""
    CMAKE_ARGS
        ${external_project_args}

        # Build shared library
        -DBUILD_SHARED_LIBS=ON
)
