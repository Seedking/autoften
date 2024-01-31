cmake_minimum_required(VERSION 3.26)
project(utils)
set(UTILS_PRJ utils)

add_library(${UTILS_PRJ} window_capture.cpp window_capture.hpp)