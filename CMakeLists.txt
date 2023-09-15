cmake_minimum_required(VERSION 3.12)

project(dawnbuild CXX C)

add_library(dawnbuild "src/dawn/webgpu_cpp.cpp")
target_include_directories(dawnbuild PUBLIC "include")

if (MSVC)
    if (CMAKE_BUILD_TYPE MATCHES Debug)
        target_link_directories(dawnbuild PUBLIC "lib/windows/x64/debug")
    else()
        target_link_directories(dawnbuild PUBLIC "lib/windows/x64/release")
    endif()
endif()

target_link_libraries(dawnbuild PUBLIC webgpu_dawn)
