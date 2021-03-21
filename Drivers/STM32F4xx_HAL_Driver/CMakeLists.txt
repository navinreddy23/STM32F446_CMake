add_library(Stm32Hal)

target_compile_definitions(Stm32Hal 
    PRIVATE
        -DUSE_HAL_DRIVER
        -D${ST_DEVICE}
)

target_compile_options(Stm32Hal
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

add_dependencies(Stm32Hal ArmCore)

target_include_directories(Stm32Hal
    PUBLIC
        Inc
        ${CMAKE_SOURCE_DIR}/Application/Inc
)

target_sources(Stm32Hal
    PUBLIC
        Src/stm32f4xx_hal_tim.c 
        Src/stm32f4xx_hal_tim_ex.c 
        Src/stm32f4xx_hal_uart.c 
        Src/stm32f4xx_hal_rcc.c 
        Src/stm32f4xx_hal_rcc_ex.c 
        Src/stm32f4xx_hal_flash.c 
        Src/stm32f4xx_hal_flash_ex.c 
        Src/stm32f4xx_hal_flash_ramfunc.c 
        Src/stm32f4xx_hal_gpio.c 
        Src/stm32f4xx_hal_dma_ex.c 
        Src/stm32f4xx_hal_dma.c 
        Src/stm32f4xx_hal_pwr.c 
        Src/stm32f4xx_hal_pwr_ex.c 
        Src/stm32f4xx_hal_cortex.c 
        Src/stm32f4xx_hal.c 
        Src/stm32f4xx_hal_exti.c 
)

target_link_libraries(Stm32Hal ArmCore)