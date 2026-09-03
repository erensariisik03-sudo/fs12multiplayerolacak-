cmake_minimum_required(VERSION 3.10)

project(MultiplayerMod)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -DTARGET_ARCH_ARM=1")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DTARGET_ARCH_ARM=1")

add_definitions(-DIMGUI_IMPL_OPENGL_ES2)

add_library(substrate SHARED IMPORTED)
set_target_properties(substrate PROPERTIES
    IMPORTED_LOCATION "${CMAKE_CURRENT_SOURCE_DIR}/libs/armeabi/libsubstrate.so"
)

add_library(multiplayermod SHARED
    yeni.cpp
    imgui/imgui.cpp
    imgui/imgui_draw.cpp
    imgui/imgui_tables.cpp
    imgui/imgui_widgets.cpp
    imgui/backends/imgui_impl_opengl3.cpp
)

target_include_directories(multiplayermod PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/imgui
    ${CMAKE_CURRENT_SOURCE_DIR}/imgui/backends
    ${CMAKE_CURRENT_SOURCE_DIR}/includes
)

target_link_libraries(multiplayermod
    substrate
    android
    log
    EGL
    GLESv2
)
