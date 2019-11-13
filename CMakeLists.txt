cmake_minimum_required(VERSION 2.8.3)
project(serial)

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
