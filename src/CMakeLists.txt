CMAKE_MINIMUM_REQUIRED(VERSION 3.0.0)

PROJECT(emscripten-glfw3-cmake-example VERSION 0.1.0)

set(CMAKE_CXX_STANDARD 11)

if (NOT EMSCRIPTEN)
    find_package(glfw3 REQUIRED)
    message("glfw found with version " ${glfw3_VERSION})
endif()

FILE(GLOB SRC
    *.cpp
    *.h) 

ADD_EXECUTABLE(${PROJECT_NAME} ${SRC} GL/src/glad.c)
TARGET_INCLUDE_DIRECTORIES(${PROJECT_NAME} PUBLIC GL/include)

if(EMSCRIPTEN)
set_target_properties(${PROJECT_NAME} PROPERTIES SUFFIX ".html")
#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -o index.html")
set_target_properties(${PROJECT_NAME} PROPERTIES LINK_FLAGS "-s USE_GLFW=3")
TARGET_LINK_LIBRARIES(${PROJECT_NAME} glfw)
else()
target_link_libraries(${PROJECT_NAME} glfw dl)
endif()


