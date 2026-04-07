---
title: Embedded Systems
type: docs
---

Embedded systems, in contrast to general-purpose computers, are designed for specific tasks and are often smaller and more resource-constrained. As of 2026, popular embedded systems include:
- STM32 microcontrollers, based on ARM RISC architecture, popular for industrial applications.
- ESP32 microcontrollers, based on ARM and RISC-V architectures, popular for IoT applications.
- Raspberry Pi single-board computers, which actually sit between embedded systems and general-purpose computers, as they can run a full operating system like Linux.

To develop for embedded systems, several frameworks and tools are commonly used:
- Arduino: A simplified C++ framework for programming microcontrollers, supporting a wide range of boards including STM32 and ESP32.
- PlatformIO: An open-source toolchain, supporting multiple frameworks(Arduino, STM32Cube, ESP-IDF, etc), usually used with VSCode editor.
- Vendor-specific SDKs: For example, STM32Cube for STM32 microcontrollers, and ESP-IDF for ESP32 microcontrollers, providing low-level access.
- RTOS: Real-time operating systems like FreeRTOS

Aside from the most popular choices of programming languages such as C and C++, there are also other languages that can be used for embedded systems, such as:
- MicroPython: supports STM32, ESP32, etc
- Rust: a safer alternative, for STM32, and also ESP32, etc
- JavaScript: Espruino supports STM32, ESP32, nrf series, etc
- JVM-based languages: with frameworks like FlintESPJVM for ESP32
- Go: with frameworks like TinyGo for STM32 and ESP32
- Scala: multiple routes towards embedded systems, such as Scala.js with Espruino, or Scala jvm with FlintESPJVM, etc

Next, we will introduce several microcontroller with different frameworks or programming languages. 

Mostly, we will focus on **PlatformIO** with Arduino framework.


## STM8 with Arduino
The STM8 microcontroller is a low-cost, 8-bit microcontroller, and running Arduino could be challenging, as only C is supported, rather than C++. The Arduino STM8 project is [sduino](https://github.com/tenbaht/sduino). It's based on SDCC, an open-source C compiler for STM8.

Quoted limitations of sduino:

    SDCC doesn't support C++. Some preprocessor magic is applied to close the gap between C and C++ syntax as much as possible, but this is not a 100% compatible drop-in replacement for full Arduino environments like for AVR or STM32


Examples for blinking, uart, etc can be found at 
- [platformio STM8 examples](https://github.com/platformio/platform-ststm8/tree/master/examples)
- [sduino examples](https://github.com/tenbaht/sduino/tree/development/examples)
- OLED, EEPROM,etc: [sduino API](https://tenbaht.github.io/sduino/api/Mini_SSD1306/)

## ESP32 with Arduino
ESP32 is popular for IoT applications with WIFI and Bluetooth, so a common use case is to build a web server on ESP32, where convenient libraries are provided for easy development with WIFI. 


A web server serving static files from SPIFFS: [ESP32 Web Server SPIFFS](https://randomnerdtutorials.com/esp32-web-server-spiffs-spi-flash-file-system/)

## ESP32 with JVM
This requires FlintESPJVM, a JVM implementation for ESP32, providing hardware access like GPIO in Java. To start efficiently, we will use Scala and VsCode. The steps are as follows:
- create a new Scala sbt project, and add the sdk as a local library dependency.
- write code in Scala, by looking at the [Java examples]()
- run the command to compile and flash the code and FlintESPJVM to the ESP32 board.

## ESP32 with JavaScript
To run JavaScript on ESP32, we can use Espruino, which is a JavaScript interpreter, as quoted from their website:

    Espruino is a JavaScript interpreter for microcontrollers. It is designed for devices with as little as 128kB Flash and 8kB RAM.

Espruino can be understood as a JavaScript version of Arduino, as it supports a wide range of microcontrollers, including STM32, ESP32, nrf series, etc.

We mainly focus on typescript and VSCode at (https://www.espruino.com/Typescript+and+Visual+Studio+Code+IDE), although the official Espruino IDE is provided. The [types for Espruino](https://www.npmjs.com/package/@types/espruino) can also be used by Scala.js.


A interesting feature in [FAQ](https://www.espruino.com/FAQ) is that `delay()` is discouraged, and call back functions in `setTimeout()` are preferred, which is common in software development, but not so common in embedded systems.

### Display
[OLED with SSD1306 driver](https://www.espruino.com/SSD1306)
