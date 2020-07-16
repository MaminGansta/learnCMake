cmake_minimum_required(VERSION 3.12)
project(MyProject VERSION 1.0.0)

#target_include_directories(MyProject PUBLIC ${})

set(SOURCES
    main.cpp
)

set(HEADERS

)

add_executable(hello_window ${SOURCES} ${HEADERS})

set_target_properties(
    hello_window PROPERTIES
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED ON
)

# add libraries
target_include_directories(
    hello_window 
    PRIVATE
    #inlcude dir
    ${CMAKE_CURRENT_SOURCE_DIR}/dependencies/glfw/include
    ${CMAKE_CURRENT_SOURCE_DIR}/dependencies/glew/include
)

target_link_directories(
    hello_window 
    PRIVATE
    #lib dir
    ${CMAKE_CURRENT_SOURCE_DIR}/dependencies/glfw/lib
    ${CMAKE_CURRENT_SOURCE_DIR}/dependencies/glew/lib
)

if (APPLE)
    target_link_libraries(
        hello_window
        libglfw3.a
        libGLEW.a
        "-framework OpenGL"
        "-framework IOKit"
        "-framework Cocoa"
        "-framework Carbon"
    )
endif()


if (WIN32)
    target_link_libraries(
        hello_window
        glfw3.lib
        glew32s.lib
        opengl32.lib
)
endif()