cmake_minimum_required (VERSION 3.8)

#include_directories( ${CMAKE_CURRENT_SOURCE_DIR}/cli ${CMAKE_CURRENT_SOURCE_DIR}/lib ${CMAKE_CURRENT_SOURCE_DIR}/package1 ${CMAKE_CURRENT_SOURCE_DIR}/package2) 
#test

project (smoketest_project) 

set(SMOKETEST_PROJECT_INCLUDE_DIRS ${CMAKE_CURRENT_SOURCE_DIR}/src ${CMAKE_CURRENT_SOURCE_DIR}/3rdparty CACHE STRING "Project include dirs")

include_directories( ${SMOKETEST_PROJECT_INCLUDE_DIRS}) 

list(APPEND CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake")

if(CMAKE_COMPILER_IS_GNUCXX)
    SET(CMAKE_CXX_FLAGS "-g -O0 -fprofile-arcs -ftest-coverage")
    include(CodeCoverage)
endif()


file(GLOB smoketest_project_SRCS
	"src/cli/*.cc" 
	"src/lib/component1.cc" 
	"3rdparty/*.cc"
)

set(SMOKETEST_PROJECT_SOURCE_FILES ${smoketest_project_SRCS} CACHE STRING "Project source files")

add_executable (smoketest_project ${smoketest_project_SRCS})

add_subdirectory( ${CMAKE_CURRENT_SOURCE_DIR}/tests )
