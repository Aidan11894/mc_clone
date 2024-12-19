# Minimum CMake version required
cmake_minimum_required(VERSION 3.10)

# Project name and language
project(mc_clone LANGUAGES C CXX)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Add executable target
add_executable(mc_clone src/main.cpp)

# Include directories for all libraries (glad, GLFW, KHR)
target_include_directories(mc_clone PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/Libraries/include)

# Add and link glad
add_library(glad ${CMAKE_CURRENT_SOURCE_DIR}/glad.c)
target_include_directories(glad PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/Libraries/include)
target_link_libraries(mc_clone PRIVATE glad)

# Link GLFW (precompiled static library)
target_link_libraries(mc_clone PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/Libraries/lib/libglfw3.a)

# Find and link OpenGL
find_package(OpenGL REQUIRED)
target_link_libraries(mc_clone PRIVATE OpenGL::GL)

# Link additional libraries for Linux
target_link_libraries(mc_clone PRIVATE X11 pthread dl)