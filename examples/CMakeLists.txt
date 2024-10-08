cmake_minimum_required(VERSION 3.16)
project(rocket_example CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_executable(example example.cpp)
target_link_libraries(example PRIVATE rocket::rocket)
