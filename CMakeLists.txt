cmake_minimum_required(VERSION 3.0.2)
project(serial VERSION 1.2.1)

# Options
option(BUILD_EXAMPLES "Build serial example" ON)

if(APPLE)
    find_library(IOKIT_LIBRARY IOKit)
    find_library(FOUNDATION_LIBRARY Foundation)
endif()

if(UNIX AND NOT APPLE)
    # If Linux, add rt and pthread
    set(rt_LIBRARIES rt)
    set(pthread_LIBRARIES pthread)
endif()

add_subdirectory(src)

## Optional targets
if(BUILD_EXAMPLES)
    add_subdirectory(examples)
endif()

if(BUILD_TESTING)
    enable_testing()

    add_subdirectory(tests)
endif()
