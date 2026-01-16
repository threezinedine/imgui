cmake_minimum_required(VERSION 3.20)

project(imgui)

file(
    GLOB 
    IMGUI_SOURCES
    "${CMAKE_CURRENT_SOURCE_DIR}/*.cpp"
)

file(
    GLOB
    IMGUI_HEADERS
    "${CMAKE_CURRENT_SOURCE_DIR}/*.h"
)

set(IMGUI_LIBS)

if (IMGUI_BACKEND_GLFW)
    list(APPEND IMGUI_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_glfw.cpp")
    list(APPEND IMGUI_HEADERS "${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_glfw.h")
    list(APPEND IMGUI_LIBS glfw)
endif()

if (IMGUI_BACKEND_OPENGL3)
    list(APPEND IMGUI_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_opengl3.cpp")
    list(APPEND IMGUI_HEADERS "${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_opengl3.h")
    list(APPEND IMGUI_LIBS OpenGL::GL)
endif()

if (IMGUI_BACKEND_VULKAN)
    list(APPEND IMGUI_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_vulkan.cpp")
    list(APPEND IMGUI_HEADERS "${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_vulkan.h")
    list(APPEND IMGUI_LIBS Vulkan::Vulkan)
endif()

if (IMGUI_BACKEND_WIN32)
    list(APPEND IMGUI_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_win32.cpp")
    list(APPEND IMGUI_HEADERS "${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_win32.h")
endif()

if (IMGUI_BACKEND_DIRECTX11)
    list(APPEND IMGUI_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_dx11.cpp")
    list(APPEND IMGUI_HEADERS "${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_dx11.h")
endif()

add_library(
    ${PROJECT_NAME} 
    STATIC 
    ${IMGUI_SOURCES} 
    ${IMGUI_HEADERS}
)

target_include_directories(
    ${PROJECT_NAME}
    PUBLIC
    "${CMAKE_CURRENT_SOURCE_DIR}/backends"
    "${CMAKE_CURRENT_SOURCE_DIR}"
)

target_link_libraries(
    ${PROJECT_NAME}
    PUBLIC
    ${IMGUI_LIBS}
)
