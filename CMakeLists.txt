cmake_minimum_required(VERSION 3.10)

project(CPP_Template LANGUAGES CXX)

set (CMAKE_CXX_STANDARD 20)
set (CMAKE_CXX_STANDARD_REQUIRED ON)
add_compile_definitions(CPP_TEMPLATE_VERSION="0.0.0") # Remember to also change it in the code and workflow

include_directories("Headers")

set(PRECOMPILED_HEADER "Headers/pch.hpp")
set(SOURCES
    "Sources/main.cpp"
)

add_executable(${PROJECT_NAME} ${SOURCES})

target_precompile_headers(${PROJECT_NAME} PRIVATE ${PRECOMPILED_HEADER})