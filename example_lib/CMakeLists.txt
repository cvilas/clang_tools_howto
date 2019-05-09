project(example_lib CXX)

include_directories(BEFORE ${PROJECT_SOURCE_DIR}/include)

file(GLOB_RECURSE this_src ${PROJECT_SOURCE_DIR}/src/*.cpp)
file(GLOB_RECURSE this_hdr ${PROJECT_SOURCE_DIR}/include/*.h)

add_library(example_lib ${this_src} ${this_hdr})
add_clang_format(example_lib)

