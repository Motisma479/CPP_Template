cmake_minimum_required(VERSION 3.10)

project(CPP_Template LANGUAGES CXX  DESCRIPTION "" VERSION 0.0.0)
string(TOUPPER ${PROJECT_NAME} PROJECT_NAME_UPPER)

set (CMAKE_CXX_STANDARD 20)
set (CMAKE_CXX_STANDARD_REQUIRED ON)

configure_file(
    ${CMAKE_SOURCE_DIR}/Headers/Core/Version.hpp.in
    ${CMAKE_BINARY_DIR}/Generated/Headers/Core/Version.hpp
    @ONLY
)

set(PRECOMPILED_HEADER "Headers/pch.hpp")
set(SOURCES
    "Sources/main.cpp"
)

if(WIN32)
    string(TIMESTAMP CURRENT_YEAR "%Y")
    set(PROJECT_AUTHOR "")
    configure_file(
        ${CMAKE_SOURCE_DIR}/app.rc.in
        ${CMAKE_BINARY_DIR}/Generated/app.rc
        @ONLY
    )

    list(APPEND SOURCES "${CMAKE_BINARY_DIR}/Generated/app.rc")
endif()

add_executable(${PROJECT_NAME} ${SOURCES})

target_include_directories(${PROJECT_NAME} PRIVATE
    ${CMAKE_SOURCE_DIR}/Headers
    ${CMAKE_BINARY_DIR}/Generated/Headers
)
target_precompile_headers(${PROJECT_NAME} PRIVATE ${PRECOMPILED_HEADER})