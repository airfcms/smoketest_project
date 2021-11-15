cmake_minimum_required (VERSION 3.8)

#include_directories( ${CMAKE_CURRENT_SOURCE_DIR}/cli ${CMAKE_CURRENT_SOURCE_DIR}/lib ${CMAKE_CURRENT_SOURCE_DIR}/package1 ${CMAKE_CURRENT_SOURCE_DIR}/package2) 

project (smoketest_project) 

include_directories( ${CMAKE_CURRENT_SOURCE_DIR}/src ${CMAKE_CURRENT_SOURCE_DIR}/3rdparty ) 

add_executable (cppcheck_project "src/cli/main.cc" "src/lib/component1.cc" "3rdparty/extlib.cc")
