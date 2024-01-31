cmake_minimum_required(VERSION 3.26)
project(autoften)

# set cpp standard version
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_subdirectory(test)
add_subdirectory(src)