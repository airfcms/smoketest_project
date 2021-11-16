cmake_minimum_required (VERSION 3.8)

#include_directories( ${CMAKE_CURRENT_SOURCE_DIR}/cli ${CMAKE_CURRENT_SOURCE_DIR}/lib ${CMAKE_CURRENT_SOURCE_DIR}/package1 ${CMAKE_CURRENT_SOURCE_DIR}/package2) 

project (runUnitTests) 

# tests
enable_testing()

include_directories(/usr/src/gtest/include /usr/src/gtest)

################################
# Unit Tests
################################

if(CMAKE_COMPILER_IS_GNUCXX)
    SET(CMAKE_CXX_FLAGS "-g -O0 -fprofile-arcs -ftest-coverage")
    setup_target_for_coverage_gcovr_xml(NAME codeCoverageAnalysis EXECUTABLE smoketest_project_tests coverage)
endif()

# Add test cpp file
add_executable( smoketest_project_tests unittests/test_component1.cc "../src/lib/component1.cc")

# Link test executable against gtest & gtest_main
target_link_libraries(smoketest_project_tests gtest gtest_main pthread gcov)

add_test( NAME unitTests COMMAND smoketest_project_tests --gtest_output=xml:${CMAKE_BINARY_DIR}/gtest-report.xml )
add_test( NAME codeCoverage COMMAND /usr/bin/gcovr --xml -r ${CMAKE_CURRENT_SOURCE_DIR}/../src --object-directory=${CMAKE_BINARY_DIR}/tests -o ${CMAKE_BINARY_DIR}/gcovr-report.xml)

separate_arguments(SMOKETEST_PROJECT_INCLUDE_DIRS)
separate_arguments(SMOKETEST_PROJECT_SOURCE_FILES)

string(REPLACE ";" " -I" L1 "${SMOKETEST_PROJECT_INCLUDE_DIRS}")
string(REPLACE ";" " " L2 "${SMOKETEST_PROJECT_SOURCE_FILES}")

add_test( NAME cppcheckAnalysis COMMAND sh -c "cppcheck -v --enable=all --xml ${L1} ${L2} 2> ${CMAKE_BINARY_DIR}/cppcheck-report.xml")
