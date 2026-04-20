# Define relevant folders
set(source_dir ${CMAKE_SOURCE_DIR}/eng/submodules/assimp)
set(build_dir ${CMAKE_BINARY_DIR}/build/assimp)
set(install_dir ${CMAKE_BINARY_DIR}/install/assimp)

# Define external project
silk_get_external_project_args(external_project_args ${install_dir})
ExternalProject_Add(External.Assimp
    SOURCE_DIR ${source_dir}
    BINARY_DIR ${build_dir}
    INSTALL_DIR ${install_dir}
    CMAKE_ARGS
        ${external_project_args}

        # Build shared library
        -DBUILD_SHARED_LIBS=ON

        # Other options
        -DASSIMP_BUILD_ZLIB=ON
        -DASSIMP_WARNINGS_AS_ERRORS=OFF
        -DASSIMP_BUILD_TESTS=OFF
)
