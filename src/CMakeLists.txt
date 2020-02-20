cmake_minimum_required(VERSION 3.0.0)

project(emscripten-glfw3-cmake-example VERSION 0.1.0)

set(CMAKE_CXX_STANDARD 11)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif()
message("CMAKE_BUILD_TYPE: ${CMAKE_BUILD_TYPE}")

option(USE_LEGACY_OPENGL "Use Legacy OpenGL (fixed function pipeline) or Modern OpenGL (with shaders)" OFF)
if(USE_LEGACY_OPENGL)
    add_definitions(-DUSE_LEGACY_OPENGL)
endif()
message("USE_LEGACY_OPENGL: ${USE_LEGACY_OPENGL}")

add_executable(${PROJECT_NAME} main.cpp GL/src/glad.c)

if(EMSCRIPTEN)
    set_target_properties(${PROJECT_NAME} PROPERTIES SUFFIX ".html")
    set(LFLAGS "-s USE_GLFW=3")
    if(USE_LEGACY_OPENGL)
        set(LFLAGS "${LFLAGS} -s LEGACY_GL_EMULATION=1")
    endif()
    set_target_properties(${PROJECT_NAME} PROPERTIES LINK_FLAGS "${LFLAGS}")
else()
    find_package(glfw3 REQUIRED)
    message("glfw found with version " ${glfw3_VERSION})
    target_link_libraries(${PROJECT_NAME} dl)
endif()
message("EMSCRIPTEN: ${EMSCRIPTEN}")
target_include_directories(${PROJECT_NAME} PRIVATE GL/include)
target_link_libraries(${PROJECT_NAME} glfw)

