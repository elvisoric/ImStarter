cmake_minimum_required(VERSION 3.14)

include(cmake/Vcpkg.cmake)

project(
    ImStarter 
    VERSION 0.0.1 
    LANGUAGES CXX
)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(PROJECT_HEADERS)
set(PROJECT_SOURCES)
set(PROJECT_MAIN main.cpp)

set(PROJECT_LIBS 
    $<TARGET_NAME_IF_EXISTS:SDL2::SDL2main>
    $<IF:$<TARGET_EXISTS:SDL2::SDL2>,SDL2::SDL2,SDL2::SDL2-static>
    imgui::imgui
    OpenGL::GL
)

find_package(SDL2 CONFIG REQUIRED)
find_package(imgui CONFIG REQUIRED)
find_package(OpenGL REQUIRED)

add_executable(${PROJECT_NAME} ${PROJECT_HEADERS} ${PROJECT_SOURCES} ${PROJECT_MAIN})

target_link_libraries(${PROJECT_NAME} PRIVATE ${PROJECT_LIBS})

