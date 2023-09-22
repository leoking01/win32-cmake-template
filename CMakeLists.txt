cmake_minimum_required(VERSION 3.20)

# Edit the BuildOptions.cmake file to change build time options
include(BuildOptions.cmake)

project(${MAIN_PROJECT_NAME})

enable_testing()

include(FetchContent)
fetchcontent_declare(
        googletest
#        URL https://github.com/google/googletest/archive/refs/heads/main.zip
 URL
#        https://github.com/google/googletest.git
#https://codeload.github.com/google/googletest/zip/refs/heads/main
https://github.com/google/googletest/archive/refs/tags/v1.14.0.zip
)
# Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
fetchcontent_makeavailable(googletest)

if (ENABLE_NOTIFICATION_ICON)
    add_compile_definitions(_ENABLE_NOTIFICATION_ICON)
endif ()

if (SINGLE_INSTANCE_ONLY)
    add_compile_definitions(_SINGLE_INSTANCE_ONLY)
endif ()

add_subdirectory(libs/supportlib)
add_subdirectory(tests/supportlib.tests)
add_subdirectory(app)
