set(EXEC_NAME Stm32Blinky)
set(EXECUTABLE ${EXEC_NAME}.elf)
add_executable(${EXECUTABLE})

target_sources(${EXECUTABLE}
    PRIVATE 
        Src/stm32f4xx_it.c
        Src/stm32f4xx_hal_msp.c
        Src/main.c
        Src/system_stm32f4xx.c
)

target_include_directories(${EXECUTABLE}
    PRIVATE
        Inc
)

target_compile_definitions(${EXECUTABLE}  
    PRIVATE
        -DUSE_HAL_DRIVER
        -D${ST_DEVICE}
)

target_link_libraries(${EXECUTABLE} Stm32Hal)

target_compile_options(${EXECUTABLE} 
    PRIVATE
        -mcpu=${CPU_ARCH}
        -mthumb
        -mfpu=fpv4-sp-d16
        -mfloat-abi=hard

        -fdata-sections
        -ffunction-sections

        -Wall

        $<$<CONFIG:Debug>:-Og>
)

target_link_options(${EXECUTABLE} 
    PRIVATE
        -T${LINKER_FILE}
        -mcpu=${CPU_ARCH}
        -mthumb
        -mfpu=fpv4-sp-d16
        -mfloat-abi=hard
        -specs=nano.specs
        -lc
        -lm
        -lnosys
        -Wl,-Map=${EXEC_NAME}.map,--cref
        -Wl,--gc-sections
)

# Print executable size
add_custom_command(TARGET ${EXECUTABLE}
        POST_BUILD
            COMMAND ${CMAKE_SIZE_UTIL} ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/${EXECUTABLE}
)

# Create hex file
add_custom_command(TARGET ${EXECUTABLE}
        POST_BUILD
            COMMAND ${CMAKE_OBJCOPY} -O ihex ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/${EXECUTABLE} ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/${EXEC_NAME}.hex
            COMMAND ${CMAKE_OBJCOPY} -O binary ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/${EXECUTABLE} ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/${EXEC_NAME}.bin
)