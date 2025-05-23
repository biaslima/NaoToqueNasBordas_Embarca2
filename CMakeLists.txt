# Generated Cmake Pico project file

cmake_minimum_required(VERSION 3.13)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Initialise pico_sdk from installed location
# (note this can come from environment, CMake cache etc)

set(PICO_BOARD pico_w CACHE STRING "Board type")

# Pull in Raspberry Pi Pico SDK (must be before project)
include(pico_sdk_import.cmake)

project(Projeto_Integrador C CXX ASM)

# Initialise the Raspberry Pi Pico SDK
pico_sdk_init()

# Add executable. Default name is the project name, version 0.1

add_executable(Projeto_Integrador 
src/Projeto_Integrador.c 
lib/ssd1306.c 
lib/buzzer.c
lib/display.c 
lib/matriz_leds.c
)

pico_set_program_name(Projeto_Integrador "Projeto_Integrador")
pico_set_program_version(Projeto_Integrador "0.1")

# Generate PIO header
pico_generate_pio_header(Projeto_Integrador ${CMAKE_CURRENT_LIST_DIR}/pio/ws2812.pio)

# Modify the below lines to enable/disable output over UART/USB
pico_enable_stdio_uart(Projeto_Integrador 0)
pico_enable_stdio_usb(Projeto_Integrador 1)

# Add the standard library to the build
target_link_libraries(Projeto_Integrador
        pico_stdlib)

# Add the standard include files to the build
target_include_directories(Projeto_Integrador PRIVATE
        ${CMAKE_CURRENT_LIST_DIR}
)

# Add any user requested libraries
target_link_libraries(Projeto_Integrador 
    hardware_adc 
    hardware_pwm
    hardware_i2c 
    hardware_pio
    hardware_gpio 
    hardware_clocks
        )

pico_add_extra_outputs(Projeto_Integrador)

