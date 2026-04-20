block()
    # Define relevant folders
    set(source_dir ${CMAKE_CURRENT_LIST_DIR}/../../../eng/submodules/sdl)
    set(build_dir ${CMAKE_BINARY_DIR}/build/sdl)
    set(install_dir ${CMAKE_BINARY_DIR}/install/sdl)

    # Define external project target
    ExternalProject_Add(External.Sdl
        SOURCE_DIR ${source_dir}
        BINARY_DIR ${build_dir}
        INSTALL_DIR ${install_dir}
        CMAKE_ARGS
            # ----- Shared options -----

            # Use release builds
            -DCMAKE_BUILD_TYPE=Release

            # Set install directory
            -DCMAKE_INSTALL_PREFIX=${install_dir}

            # ----- Dependency specific options -----

            # Build shared library
            -DBUILD_SHARED_LIBS=ON

            # Other options
            # TODO: Currently based on the Linux settings used in Silk 3
            -DSDL_TEST_LIBRARY=OFF
    )
endblock()
