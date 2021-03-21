cmake_minimum_required (VERSION 3.15)

set(CMAKE_TRY_COMPILE_TARGET_TYPE "STATIC_LIBRARY")

enable_language(C ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS OFF)

set(CMAKE_TOOLCHAIN_FILE ${CMAKE_SOURCE_DIR}/cmake/arm-none-eabi-gcc.cmake)

#Output directory
set (CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/Debug)

project(HelloSTM32)

set(ST_DEVICE STM32F446xx CACHE INTERNAL "STM MCU")
set(CPU_ARCH cortex-m4 CACHE INTERNAL "ARM CPU")

add_subdirectory(System)
add_subdirectory(Drivers)
add_subdirectory(Application)