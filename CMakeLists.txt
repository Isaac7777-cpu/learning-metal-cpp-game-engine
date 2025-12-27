cmake_minimum_required(VERSION 3.28.0)
project(metal_learning VERSION 0.1.0)
project(metal_learning LANGUAGES CXX OBJCXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON) # For getting a compile_commands.json

add_executable(metal_learning
    src/main.cpp
)

target_include_directories(metal_learning
    PRIVATE
    ${CMAKE_SOURCE_DIR}/vendor/metal-cpp
)

find_library(METAL Metal)
find_library(FOUNDATION Foundation)
find_library(QUARTZCORE QuartzCore)
find_library(APPKIT AppKit)

target_link_libraries(metal_learning 
    stdc++ 
    "-framework Metal" 
    "-framework Foundation" 
    "-framework QuartzCore"
    "-framework AppKit" objc
    "-framework MetalKit"
)

execute_process(
  COMMAND ${CMAKE_COMMAND} -E create_symlink
          "${CMAKE_BINARY_DIR}/compile_commands.json"
          "${CMAKE_SOURCE_DIR}/compile_commands.json"
)

