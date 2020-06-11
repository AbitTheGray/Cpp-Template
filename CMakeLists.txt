cmake_minimum_required(VERSION 3.16)
project(Template C CXX)

set(CMAKE_CXX_STANDARD 20)
set(BUILD_SHARED_LIBS OFF)

cmake_policy(SET CMP0077 NEW) # set() overrides option()

#--------------------------------
# Debug Options
#--------------------------------

add_compile_options("$<$<CONFIG:DEBUG>:-DDEBUG>") # Define DEBUG in Debug builds

#--------------------------------
# Compiler configuration
#--------------------------------

if(MINGW)
    ADD_COMPILE_OPTIONS(-lstdc++fs)
    set(WIN32 ON)
endif()

#--------------------------------
# External libraries
#--------------------------------

add_subdirectory(lib)

#--------------------------------
# Source
#--------------------------------

file(GLOB_RECURSE PROJECT_SOURCE src/*.hpp src/*.cpp src/*.h src/*.c)

add_library(Template STATIC ${PROJECT_SOURCE})
target_include_directories(Template PUBLIC src/)

target_link_libraries(Template -static-libgcc -static-libstdc++ stdc++fs)

#--------------------------------
# Source
#--------------------------------

if(BUILD_TESTING)
    add_subdirectory(tests)
endif()