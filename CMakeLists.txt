cmake_minimum_required(VERSION 3.20)

project(responsibility-driven-dev LANGUAGES CXX)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

add_executable(responsibility-driven-dev
    src/main.cpp
)

target_compile_features(responsibility-driven-dev PRIVATE cxx_std_20)

if(CMAKE_CXX_COMPILER_ID MATCHES "Clang|GNU")
    target_compile_options(responsibility-driven-dev PRIVATE -Wall -Wextra -Wpedantic)
endif()

include(CTest)

if(BUILD_TESTING)
    find_package(GTest QUIET)
    if(NOT GTest_FOUND)
        include(FetchContent)
        set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
        FetchContent_Declare(
            googletest
            GIT_REPOSITORY https://github.com/google/googletest.git
            GIT_TAG v1.17.0
            GIT_SHALLOW TRUE
        )
        FetchContent_MakeAvailable(googletest)
    endif()

    add_executable(dummy_test
        tests/dummy_test.cpp
    )
    target_compile_features(dummy_test PRIVATE cxx_std_20)
    target_link_libraries(dummy_test PRIVATE GTest::gtest_main)

    include(GoogleTest)
    gtest_discover_tests(dummy_test)
endif()