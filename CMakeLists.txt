cmake_minimum_required(VERSION 3.0.0)
project(main VERSION 0.1.0)

# SDL2
add_subdirectory(lib/SDL)

# ImGui
file(GLOB IMGUI_SRC
    lib/imgui/*.cpp
    lib/imgui/*.h
)
set(IMGUI_BACKEND
    lib/imgui/backends/imgui_impl_sdl.cpp
    lib/imgui/backends/imgui_impl_sdl.h
    lib/imgui/backends/imgui_impl_sdlrenderer.cpp
    lib/imgui/backends/imgui_impl_sdlrenderer.h
)
add_library(ImGui ${IMGUI_SRC} ${IMGUI_BACKEND})
target_include_directories(ImGui PUBLIC "lib/imgui/")
target_link_libraries(ImGui SDL2-static)

# Main
add_executable(${PROJECT_NAME} main.cpp)
target_link_libraries(${PROJECT_NAME} ImGui)
include_directories(
    "lib/imgui/backends/"
)
