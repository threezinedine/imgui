cmake_minimum_required(VERSION 3.0)

project(ImGui)

file(
    GLOB 
    IMGUI_SRC
    ./*.cpp
    ./backends/imgui_impl_opengl3.cpp
    ./backends/imgui_impl_glfw.cpp
)


add_library(
    ${PROJECT_NAME} 
    STATIC 
    ${IMGUI_SRC}
)

target_include_directories(
    ${PROJECT_NAME}
    PUBLIC
    ./
    ./backends
)

target_link_libraries(
    ${PROJECT_NAME}
    PRIVATE
    glfw
)