# STM32_Project_W5500_TCP_Server

A TCP server over Ethernet running on an STM32F401CCU6, using the W5500 Ethernet controller over SPI. The W5500's hardware TCP/IP stack handles the network layers, so the MCU only deals with sockets and application logic.

## Features
- W5500 initialization with hardware reset and chip-select control
- TCP/IP offloaded to the W5500's hardware stack
- TCP server that accepts client connections and exchanges data
- UART debug output at 115200 baud
- Built with STM32CubeIDE and the STM32 HAL

## Hardware
| Component | Details |
|-----------|---------|
| MCU | STM32F401CCU6 (Black Pill) |
| Ethernet | W5500 module |
| System clock | 72 MHz (HSI -> PLL) |
| W5500 interface | SPI1, master, mode 0, MSB first, ~18 MHz |
| Debug | USART1, 115200 8N1 |
| Programmer | ST-Link |

## Project structure
```
Core/
  Src/
    main.c            # Peripheral init, W5500 init, starts the server
    wizchip_port.c    # SPI, chip-select and reset glue for the W5500
    tcp_server.c      # TCP server loop
  Inc/
    wizchip_port.h
    tcp_server.h
```

## How it works
1. `HAL_Init()` and system clock setup, then GPIO, SPI and UART init
2. `W5500_Init()` resets the chip and configures the network
3. `tcp_server_blocking_loop()` opens a socket, listens, and serves connected clients

## Getting started
1. Clone the repository and open it in STM32CubeIDE.
2. Build the project and flash it with ST-Link.
3. Connect the W5500 module to your router or directly to your PC with an Ethernet cable.
4. Open a serial terminal at 115200 baud to see the debug output.
5. Connect to the board with any TCP client, such as `nc`, using the device's IP address.

## Roadmap
- [ ] Firmware updates over Ethernet (OTA)

## Acknowledgements
Thanks to [ControllersTech](https://www.youtube.com/@ControllersTech) for their STM32 and W5500 Ethernet tutorials, which helped me get started.
