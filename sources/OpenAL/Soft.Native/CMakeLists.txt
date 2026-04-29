# Define relevant folders
set(source_dir ${CMAKE_SOURCE_DIR}/eng/submodules/openal-soft)
set(build_dir ${CMAKE_BINARY_DIR}/build/openal-soft)
set(install_dir ${CMAKE_BINARY_DIR}/install/openal-soft)

# Define external project
silk_get_external_project_args(external_project_args ${install_dir})
ExternalProject_Add(External.OpenAlSoft
    SOURCE_DIR ${source_dir}
    BINARY_DIR ${build_dir}
    INSTALL_DIR ${install_dir}
    DOWNLOAD_COMMAND ""
    CMAKE_ARGS
        ${external_project_args}

        # Build shared library
        -DBUILD_SHARED_LIBS=ON

        # Unnecessary features
        -DALSOFT_UTILS=OFF
        -DALSOFT_EXAMPLES=OFF

        # Other options
        # TODO: Currently based on the Linux settings used in Silk 3
        -DALSOFT_REQUIRE_RTKIT=ON
        -DALSOFT_REQUIRE_ALSA=ON
        -DALSOFT_REQUIRE_OSS=ON
        -DALSOFT_REQUIRE_PORTAUDIO=ON
        -DALSOFT_REQUIRE_PULSEAUDIO=ON
        -DALSOFT_REQUIRE_JACK=ON
        -DALSOFT_REQUIRE_PIPEWIRE=ON
)
