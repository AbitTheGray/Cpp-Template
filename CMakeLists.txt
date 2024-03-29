cmake_minimum_required(VERSION 3.16)
project(Template C CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_DISABLE_IN_SOURCE_BUILD ON)

set(CMAKE_POLICY_DEFAULT_CMP0077 NEW) # set() overrides option()



#--------------------------------
# Compiler configuration
#--------------------------------

add_compile_options("$<$<CONFIG:DEBUG>:-DDEBUG>") # Define DEBUG in Debug builds



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

if (CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
    target_link_libraries(Template -static-libgcc -static-libstdc++)
endif()



#--------------------------------
# Tests
#--------------------------------

if(BUILD_TESTING)
    enable_testing()

    add_subdirectory(tests)
endif()
