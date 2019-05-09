# note: cmake version 3.6 or above is required for clang-tidy support.
cmake_minimum_required(VERSION 3.6)
project(clang_tools_example CXX)

#----------------------------------------------------------------------------------------------------------------------
# Build system configuration files
#----------------------------------------------------------------------------------------------------------------------
include(${CMAKE_SOURCE_DIR}/cmake/colours.cmake)
include(${CMAKE_SOURCE_DIR}/cmake/add_clang_format.cmake)
set(CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake/modules)

#----------------------------------------------------------------------------------------------------------------------
# Configure linter
#----------------------------------------------------------------------------------------------------------------------

if(NOT CMAKE_CROSSCOMPILING) # adds invalid paths otherwise
    find_package(ClangTools QUIET)
    if(CLANG_TIDY_FOUND)
        set(CMAKE_CXX_CLANG_TIDY "${CLANG_TIDY_BIN};-checks=*, -fuchsia*, -google*")
    else(CLANG_TIDY_FOUND)
        message(STATUS "${Yellow}clang-tidy not found. Static analysis won't be done.${ColourReset}")
    endif(CLANG_TIDY_FOUND)
    if(NOT CLANG_FORMAT_FOUND)
        message(STATUS "${Yellow}clang-format not found. Style checks won't be done.${ColourReset}")
    endif(NOT CLANG_FORMAT_FOUND)
endif(NOT CMAKE_CROSSCOMPILING)

#----------------------------------------------------------------------------------------------------------------------
# targets
#----------------------------------------------------------------------------------------------------------------------

add_subdirectory(example_lib)
add_subdirectory(example_exe)
