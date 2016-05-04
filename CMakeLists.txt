cmake_minimum_required(VERSION 2.8)
PROJECT(snappy)

# version 
set(SNAPPY_MAJOR 1)
set(SNAPPY_MINOR 1)
set(SNAPPY_PATCHLEVEL 3)


set(SRCS 
    snappy.cc
    snappy-sinksource.cc
    snappy-stubs-internal.cc
    snappy-c.cc)

if(WIN32)
    add_definitions(-DHAVE_WINDOWS_H)
endif()

add_library(snappy ${SRCS})

if(BUILD_TESTS)
    ENABLE_TESTING()
    find_package(GTest)
    add_definitions(-DHAVE_GTEST)
    include_directories(${GTEST_INCLUDE_DIRS})
    add_executable(snappy_unittest
        snappy_unittest.cc
        snappy-test.cc)

    target_link_libraries(snappy_unittest
        snappy
        ${GTEST_BOTH_LIBRARIES})
endif()
