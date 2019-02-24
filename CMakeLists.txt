cmake_minimum_required(VERSION 3.5 FATAL_ERROR)

project(recipe-08 LANGUAGES CXX)

set(CMAKE_BUILD_TYPE DEBUG)
message("C++ compiler flags: ${CMAKE_CXX_FLAGS}")

list(APPEND flags "-fPIC" "-Wall")
if(NOT WIN32)
    list(APPEND flags "-Wextra" "-Wpedantic" "-Werror")
endif()

add_library(geometry
    STATIC
        geometry_circle.cpp
        geometry_circle.hpp
        geometry_polygon.cpp
        geometry_polygon.hpp
        geometry_rhombus.cpp
        geometry_rhombus.hpp
        geometry_square.cpp
        geometry_square.hpp
)

target_compile_options(geometry
    PRIVATE
        ${flags}
)
set_target_properties(geometry
    PROPERTIES
        CXX_STANDARD 11
        CXX_EXTENSIONS OFF
        CXX_STANDARD_REQUIRED ON
        POSITION_INDEPENDENT_CODE 1
)
add_executable(compute-areas compute-areas.cpp)

target_compile_options(compute-areas
    PRIVATE
        "-fPIC"
)

target_link_libraries(compute-areas geometry)
