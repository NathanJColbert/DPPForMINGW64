cmake_minimum_required(VERSION 4.0.2)
project(MyBot LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

add_compile_options(-w)

set(DPP_BUILD_TEST OFF CACHE BOOL "" FORCE)
add_subdirectory(external/dpp)

# ---------------------------------
# Use this
# file(GLOB SRC_FILES src/*.cpp)
# add_executable(MyBot ${SRC_FILES})
# ---------------------------------

# ---------------------------------
# Or this
add_executable(MyBot
    src/main.cpp
    # Add *.cpp files here
)
# ---------------------------------

target_include_directories(MyBot PRIVATE 
    include
    external/dpp/include
)

target_link_libraries(MyBot PRIVATE 
    dpp 
    ws2_32 
    winmm
)

add_custom_command(TARGET MyBot POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
        $<TARGET_FILE:dpp>
        $<TARGET_FILE_DIR:MyBot>
)