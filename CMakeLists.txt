cmake_policy(SET CMP0048 NEW)
project(Minecraft VERSION 0.0.1)
cmake_minimum_required(VERSION 3.25)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_FLAGS "-O2 -g -Wall -Wextra -Wpedantic -Wno-c99-extensions")
set(CMAKE_BINARY_DIR ${CMAKE_SOURCE_DIR}/bin)
set(CMAKE_CURRENT_BINARY_DIR ${CMAKE_BINARY_DIR})

#--------------------------------------
# BGFX
#--------------------------------------
add_subdirectory(lib/bgfx.cmake)
include_directories(lib/bgfx.cmake/bgfx/include)
include_directories(lib/bgfx.cmake/bx/include)
include_directories(lib/bgfx.cmake/bimg/include)
include_directories(lib/bgfx.cmake/bgfx/3rdparty/fcpp)

#--------------------------------------
# GLFW
#--------------------------------------
add_subdirectory(lib/glfw)
include_directories(lib/glfw/include)

#--------------------------------------
# GLM
#--------------------------------------
add_subdirectory(lib/glm)

#--------------------------------------
# Noise 
#--------------------------------------
add_subdirectory(lib/noise)
include_directories(lib/noise)

#--------------------------------------
# tomlplusplus
#--------------------------------------
add_subdirectory(lib/tomlplusplus)
include_directories(lib/tomlplusplus)

#--------------------------------------
# shaders
#--------------------------------------


#--------------------------------------
# Game
#--------------------------------------
include_directories(src)
file(GLOB_RECURSE game_SRC CONFIGURE_DEPENDS "src/*.c" "src/*.h" "src/*.cpp" "src/*.hpp")

add_executable(game ${game_SRC})

target_link_libraries(game bgfx glfw glm noise)
