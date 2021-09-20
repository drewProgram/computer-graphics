cmake_minimum_required(VERSION 3.10)

project(ComputerGraphics VERSION 1.0)

configure_file(src/CPConfig.h.in CPConfig.h)

# C++ version
set(CMAKE_CPP_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Setting the external libs and paths
set(__BIN_PATH ${PROJECT_SOURCE_DIR}/build/windows/x64/bin)
## GLFW
set(__GLFW_LIB_PATH ${PROJECT_SOURCE_DIR}/Dependencies/GLFW/lib-vc2019)
set(__GLFW_INCLUDE_PATH ${PROJECT_SOURCE_DIR}/Dependencies/GLFW/include)

set(__GLFW_LIB_NAME "glfw3.lib")

## GLEW
set(__GLEW_LIB_PATH ${PROJECT_SOURCE_DIR}/Dependencies/GLEW/lib)
set(__GLEW_INCLUDE_PATH ${PROJECT_SOURCE_DIR}/Dependencies/GLEW/include)

set(__GLEW_LIB_NAME "glew32s.lib")

# install the exe in this path
set(EXECUTABLE_OUTPUT_PATH ${__BIN_PATH})

## Set global definitions to be used in c++
add_definitions(-DGLEW_STATIC)

## Link Subdirectory 
add_subdirectory(${PROJECT_SOURCE_DIR}/src ${__BIN_PATH})
