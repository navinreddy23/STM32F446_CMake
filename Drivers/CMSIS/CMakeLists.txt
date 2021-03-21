add_library(ArmCore)

target_include_directories(ArmCore
    PUBLIC
        Include
        Device/ST/STM32F4xx/Include
)

target_sources(ArmCore
    PRIVATE 
        Device/ST/STM32F4xx/Source/Templates/arm/startup_stm32f446xx.s
)