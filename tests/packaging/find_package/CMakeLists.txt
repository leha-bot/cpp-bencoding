cmake_minimum_required(VERSION 3.10)
project(bencoding-check-find-package)

find_package(bencoding REQUIRED)

add_executable(test-find-package ../test.cpp)
target_link_libraries(test-find-package bencoding::bencoding)

