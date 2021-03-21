cmake_minimum_required (VERSION 3.15)

set(CMAKE_TRY_COMPILE_TARGET_TYPE "STATIC_LIBRARY")

#This does not seem to work with Qt!
#set(CMAKE_TOOLCHAIN_FILE ${CMAKE_SOURCE_DIR}/cmake/arm-none-eabi-gcc.cmake)

#set(CMAKE_MAKE_PROGRAM /usr/bin/ninja)

#Qt version. Set your toolchain directory below
set(ARM_BIN_DIR /opt/gcc-arm-none-eabi-10-2020-q4-major/bin/arm-none-eabi-)

set(CMAKE_C_COMPILER ${ARM_BIN_DIR}gcc)
set(CMAKE_ASM_COMPILER ${CMAKE_C_COMPILER})
set(CMAKE_CXX_COMPILER ${ARM_BIN_DIR}g++)

#These commands are used to generate HEX and BIN files.
set(CMAKE_SIZE_UTIL ${ARM_BIN_DIR}size)
set(CMAKE_OBJCOPY ${ARM_BIN_DIR}objcopy)

enable_language(C ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS OFF)

#Output directory
set (CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/Debug)

project(HelloSTM32)

set(ST_DEVICE STM32F446xx CACHE INTERNAL "STM MCU")
set(CPU_ARCH cortex-m4 CACHE INTERNAL "ARM CPU")

add_subdirectory(System)
add_subdirectory(Drivers)
add_subdirectory(Application)
