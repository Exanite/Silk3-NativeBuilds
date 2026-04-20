block()
    # Define relevant folders
    set(source_dir ${CMAKE_CURRENT_LIST_DIR}/../../../eng/submodules/openal-soft)
    set(build_dir ${CMAKE_BINARY_DIR}/build/openal-soft)
    set(install_dir ${CMAKE_BINARY_DIR}/install/openal-soft)

    # Define external project target
    ExternalProject_Add(External.OpenAlSoft
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
            -DALSOFT_UTILS=OFF
            -DALSOFT_EXAMPLES=OFF

            -DALSOFT_REQUIRE_RTKIT=ON
            -DALSOFT_REQUIRE_ALSA=ON
            -DALSOFT_REQUIRE_OSS=ON
            -DALSOFT_REQUIRE_PORTAUDIO=ON
            -DALSOFT_REQUIRE_PULSEAUDIO=ON
            -DALSOFT_REQUIRE_JACK=ON
            -DALSOFT_REQUIRE_PIPEWIRE=ON
    )
endblock()
