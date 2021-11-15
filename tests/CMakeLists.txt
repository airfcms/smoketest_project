cmake_minimum_required (VERSION 3.8)

#include_directories( ${CMAKE_CURRENT_SOURCE_DIR}/cli ${CMAKE_CURRENT_SOURCE_DIR}/lib ${CMAKE_CURRENT_SOURCE_DIR}/package1 ${CMAKE_CURRENT_SOURCE_DIR}/package2) 

project (runUnitTests) 

# tests
enable_testing()

include_directories(/usr/src/gtest/include /usr/src/gtest)

################################
# Unit Tests
################################
# Add test cpp file
add_executable( runUnitTests unittests/test_component1.cc "../src/lib/component1.cc")
# Link test executable against gtest & gtest_main
target_link_libraries(runUnitTests gtest gtest_main pthread)
add_test( runUnitTests runUnitTests )
