cmake_minimum_required (VERSION 3.8)

#include_directories( ${CMAKE_CURRENT_SOURCE_DIR}/cli ${CMAKE_CURRENT_SOURCE_DIR}/lib ${CMAKE_CURRENT_SOURCE_DIR}/package1 ${CMAKE_CURRENT_SOURCE_DIR}/package2) 

project (unit_tests) 

# tests
enable_testing()

include_directories(${gtest_SOURCE_DIR}/include ${gtest_SOURCE_DIR})

################################
# Unit Tests
################################
# Add test cpp file
add_executable( runUnitTests testgtest.cpp )
# Link test executable against gtest & gtest_main
target_link_libraries(runUnitTests gtest gtest_main)
add_test( runUnitTests runUnitTests )
