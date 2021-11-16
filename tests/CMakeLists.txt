cmake_minimum_required (VERSION 3.8)

#include_directories( ${CMAKE_CURRENT_SOURCE_DIR}/cli ${CMAKE_CURRENT_SOURCE_DIR}/lib ${CMAKE_CURRENT_SOURCE_DIR}/package1 ${CMAKE_CURRENT_SOURCE_DIR}/package2) 

project (runUnitTests) 

#set(GTEST_OUTPUT "xml:${CMAKE_BINARY_DIR}/testCase1.xml")

# tests
enable_testing()

include_directories(/usr/src/gtest/include /usr/src/gtest)

################################
# Unit Tests
################################

if(CMAKE_COMPILER_IS_GNUCXX)
    SET(CMAKE_CXX_FLAGS "-g -O0 -fprofile-arcs -ftest-coverage")
    setup_target_for_coverage_gcovr_xml(NAME runUnitTestsWithCoverage EXECUTABLE smoketest_project_tests coverage)
endif()

# Add test cpp file
add_executable( smoketest_project_tests unittests/test_component1.cc "../src/lib/component1.cc")
# Link test executable against gtest & gtest_main
target_link_libraries(smoketest_project_tests gtest gtest_main pthread gcov)
add_test( runUnitTests smoketest_project_tests  )
