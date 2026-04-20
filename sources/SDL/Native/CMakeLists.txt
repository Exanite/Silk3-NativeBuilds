block()
    # Define relevant folders
    set(source_dir ${CMAKE_CURRENT_LIST_DIR}/../../../eng/submodules/sdl)
    set(build_dir ${CMAKE_BINARY_DIR}/build/sdl)
    set(install_dir ${CMAKE_BINARY_DIR}/install/sdl)

    # Define external project target
    silk_get_external_project_args(external_project_args ${install_dir})
    ExternalProject_Add(External.Sdl
        SOURCE_DIR ${source_dir}
        BINARY_DIR ${build_dir}
        INSTALL_DIR ${install_dir}
        CMAKE_ARGS
            # ----- Shared options -----

            ${external_project_args}

            # ----- Dependency specific options -----

            # Build shared library
            -DBUILD_SHARED_LIBS=ON

            # Other options
            # TODO: Currently based on the Linux settings used in Silk 3
            -DSDL_TEST_LIBRARY=OFF
    )
endblock()
