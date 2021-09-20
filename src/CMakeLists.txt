cmake_minimum_required(VERSION 3.10)

# source and headers
include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${__GLEW_INCLUDE_PATH})
include_directories(${__GLFW_INCLUDE_PATH})

# find all source and header files to compile into object files
file(GLOB_RECURSE SOURCES *.cpp *.h *.c)

# add libs
## GLEW
add_library(glew STATIC IMPORTED)
set_property(TARGET glew PROPERTY IMPORTED_LOCATION "${__GLEW_LIB_PATH}/${__GLEW_LIB_NAME}")

## GLFW
add_library(glfw STATIC IMPORTED)
set_property(TARGET glfw PROPERTY IMPORTED_LOCATION "${__GLFW_LIB_PATH}/${__GLFW_LIB_NAME}")

# find required packages
find_package(OpenGL REQUIRED)

# source file containing the "main" function
set(MAIN_SOURCE Application.cpp)
# specify the name for the generated exe file
set(MAIN_EXE_NAME ${PROJECT_NAME})

# 1. compile
add_executable(${MAIN_EXE_NAME} ${MAIN_SOURCE} ${SOURCES})

# 2. link
target_include_directories(${MAIN_EXE_NAME} PUBLIC
    "${PROJECT_BINARY_DIR}"
)
target_link_libraries(${MAIN_EXE_NAME} glew glfw ${OPENGL_gl_LIBRARY})

# 3. install rules
install(TARGETS ${MAIN_EXE_NAME})
install(FILES "${PROJECT_BINARY_DIR}/CPConfig.h"
    DESTINATION include
)