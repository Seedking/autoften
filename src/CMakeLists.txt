cmake_minimum_required(VERSION 3.26)
project(src)
set(SRC_PRJ src)

add_executable(${SRC_PRJ} autoften.cpp)

# link lib
add_subdirectory(utils)
target_link_libraries(${SRC_PRJ} utils)

