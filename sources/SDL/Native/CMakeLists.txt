block()
    # Define relevant folders
    set(source_dir ${CMAKE_CURRENT_LIST_DIR}/../../../eng/submodules/sdl)
    set(build_dir ${CMAKE_BINARY_DIR}/build/sdl)
    set(install_dir ${CMAKE_BINARY_DIR}/install/sdl)

    # Define outputs
    set(base_name "SDL3")
    if(WIN32)
        set(output_binary "${install_dir}/bin/${CMAKE_SHARED_LIBRARY_PREFIX}${base_name}${CMAKE_SHARED_LIBRARY_SUFFIX}")
        set(output_lib "${install_dir}/lib/${CMAKE_IMPORT_LIBRARY_PREFIX}${base_name}${CMAKE_IMPORT_LIBRARY_SUFFIX}")
    else()
        set(output_binary "${install_dir}/lib/${CMAKE_SHARED_LIBRARY_PREFIX}${base_name}${CMAKE_SHARED_LIBRARY_SUFFIX}")
    endif()

    # Define external project target
    ExternalProject_Add(External.Sdl
        SOURCE_DIR ${source_dir}
        BINARY_DIR ${build_dir}
        INSTALL_DIR ${install_dir}
        BUILD_BYPRODUCTS
            ${output_file}
            ${output_lib}
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
            -DSDL_TEST_LIBRARY=OFF
    )
endblock()
