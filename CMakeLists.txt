cmake_minimum_required(VERSION 3.10)
project(KeplerElements)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

if(CMAKE_CXX_COMPILER_ID STREQUAL "GNU" OR CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
    add_compile_options(-Wall -Wextra -Wpedantic -g)
endif()

find_package(Eigen3 REQUIRED)

add_library(OrbitLib STATIC 
    KepToRV.cpp 
    KepToRV.hpp 
    RVToKep.cpp 
    RVToKep.hpp 
    KeplerElements.hpp
)

target_link_libraries(OrbitLib PUBLIC Eigen3::Eigen)

add_executable(KeplerElements main.cpp)
target_link_libraries(KeplerElements PRIVATE OrbitLib)
