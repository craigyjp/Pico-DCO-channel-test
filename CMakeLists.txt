cmake_minimum_required(VERSION 3.13)

include(pico_sdk_import.cmake)

project(pico-dco-ch C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

pico_sdk_init()

add_executable(pico-dco-ch
  pico-dco-ch.c
  usb_descriptors.c
)

pico_generate_pio_header(pico-dco-ch ${CMAKE_CURRENT_LIST_DIR}/pico-dco-ch.pio)

pico_enable_stdio_usb(pico-dco-ch 0)
pico_enable_stdio_uart(pico-dco-ch 1)

target_include_directories(pico-dco-ch PRIVATE ${CMAKE_CURRENT_LIST_DIR})
target_link_libraries(pico-dco-ch PRIVATE pico_stdlib hardware_pio hardware_flash hardware_adc hardware_pwm tinyusb_device tinyusb_board)

target_compile_definitions(pico-dco-ch PRIVATE
    PICO_DEFAULT_UART_TX_PIN=0
    PICO_DEFAULT_UART_RX_PIN=1
 )

pico_add_extra_outputs(pico-dco-ch)
