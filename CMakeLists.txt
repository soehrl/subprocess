cmake_minimum_required(VERSION 3.1)

if (NOT DEFINED SUBPROCESS_MAIN_PROJECT)
  set(SUBPROCESS_MAIN_PROJECT OFF)
  if (CMAKE_CURRENT_SOURCE_DIR STREQUAL CMAKE_SOURCE_DIR)
    set(SUBPROCESS_MAIN_PROJECT ON)
  endif ()
endif ()

option(SUBPROCESS_BUILD_TESTS "Build the tests in the project" ${SUBPROCESS_MAIN_PROJECT})

project(subprocess CXX)

set(CMAKE_CXX_STANDARD 11)

include(CTest)

if (SUBPROCESS_BUILD_TESTS)
  add_subdirectory(test)
endif()

add_library(subprocess INTERFACE)
add_library(subprocess::subprocess ALIAS subprocess)

target_include_directories(subprocess INTERFACE .)

install(
  FILES subprocess.hpp
  TYPE INCLUDE
)
