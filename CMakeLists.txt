cmake_minimum_required(VERSION 3.0.0)
project(main)

set(sf main.cpp)

find_package(SDL2 REQUIRED)
find_library(SDL2_NET_LIBRARY SDL2_net)

if (NOT SDL2_NET_LIBRARY)
    message(FATAL_ERROR "SDL2_net library not found")
endif()

include_directories(${SDL2_INCLUDE_DIRS})
add_executable(${PROJECT_NAME} ${sf})
target_link_libraries(${PROJECT_NAME} ${SDL2_LIBRARIES} ${SDL2_NET_LIBRARY})
