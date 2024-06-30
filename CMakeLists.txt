cmake_minimum_required(VERSION 3.12)

project(dawnbuild CXX C)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_EXTENSIONS NO)
set(CMAKE_CXX_STANDARD_REQUIRED YES)

add_library(dawnbuild INTERFACE)
target_include_directories(dawnbuild INTERFACE "include")

if (MSVC)
    if (CMAKE_BUILD_TYPE MATCHES Debug)
        target_link_directories(dawnbuild INTERFACE "lib/windows/debug")
    else()
        target_link_directories(dawnbuild INTERFACE "lib/windows/release")
    endif()
endif()

if (APPLE)
    if (CMAKE_BUILD_TYPE MATCHES Debug)
        target_link_directories(dawnbuild INTERFACE "lib/macOS/debug")
    else()
        target_link_directories(dawnbuild INTERFACE "lib/macOS/release")
    endif()
endif()

if (UNIX)
    if (CMAKE_BUILD_TYPE MATCHES Debug)
        target_link_directories(dawnbuild INTERFACE "lib/linux/debug")
    else()
        target_link_directories(dawnbuild INTERFACE "lib/linux/release")
    endif()
endif()

target_link_libraries(dawnbuild INTERFACE webgpu_dawn)
