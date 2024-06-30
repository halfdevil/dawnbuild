cmake_minimum_required(VERSION 3.12)

project(dawnbuild CXX C)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_EXTENSIONS NO)
set(CMAKE_CXX_STANDARD_REQUIRED YES)

add_library(dawnbuild "src/dawn/webgpu_cpp.cpp")
target_include_directories(dawnbuild PUBLIC "include")

if (MSVC)
    if (CMAKE_BUILD_TYPE MATCHES Debug)
        target_link_directories(dawnbuild PUBLIC "lib/windows/debug")
    else()
        target_link_directories(dawnbuild PUBLIC "lib/windows/release")
    endif()
endif()

if (APPLE)
    if (CMAKE_BUILD_TYPE MATCHES Debug)
        target_link_directories(dawnbuild PUBLIC "lib/macOS/debug")
    else()
        target_link_directories(dawnbuild PUBLIC "lib/macOS/release")
    endif()
endif()

if (UNIX)
    if (CMAKE_BUILD_TYPE MATCHES Debug)
        target_link_directories(dawnbuild PUBLIC "lib/linux/debug")
    else()
        target_link_directories(dawnbuild PUBLIC "lib/linux/release")
    endif()
endif()

target_link_libraries(dawnbuild PUBLIC webgpu_dawn)
