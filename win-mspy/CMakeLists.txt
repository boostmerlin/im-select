cmake_minimum_required(VERSION 3.10)

project(im-select-mspy)


set(CMAKE_CXX_STANDARD 17)

if(NOT DEFINED CMAKE_GENERATOR_PLATFORM)
    set(CMAKE_GENERATOR_PLATFORM "x64") # 或者 "Win32", "ARM", 等等
endif()
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/${CMAKE_GENERATOR_PLATFORM}/${CMAKE_BUILD_TYPE})

add_executable(im-select-mspy main.cc)
target_link_libraries(im-select-mspy comsuppw.lib)

