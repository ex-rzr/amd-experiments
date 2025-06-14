cmake_minimum_required(VERSION 3.26 FATAL_ERROR)

project(gpu-experiments LANGUAGES CXX HIP)
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_HIP_STANDARD 23)

include(FetchContent)

FetchContent_Declare(
    rocm_smi
    GIT_REPOSITORY https://github.com/ROCm/rocm_smi_lib
    GIT_TAG rocm-6.4.1
    OVERRIDE_FIND_PACKAGE
)

find_package(rocm_smi REQUIRED)

add_executable(arithmetic arithmetic.hip)
target_link_libraries(arithmetic PRIVATE stdc++_libbacktrace rocm_smi64)

add_executable(atomic_local atomic_local.hip)
target_link_libraries(atomic_local PRIVATE stdc++_libbacktrace rocm_smi64)

add_executable(atomic_global atomic_global.hip)
target_link_libraries(atomic_global PRIVATE stdc++_libbacktrace rocm_smi64)

add_executable(memory memory.hip)
target_link_libraries(memory PRIVATE stdc++_libbacktrace rocm_smi64)

add_executable(shuffle shuffle.hip)
target_link_libraries(shuffle PRIVATE stdc++_libbacktrace rocm_smi64)
