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

## Prerequisites
**Arduino and PlatformIO basics**
The Arduino framework mandates two main functions: `setup()` and `loop()`. The `setup()` function is called once when the program starts, and is used to initialize variables, pin modes, etc. The `loop()` function is called repeatedly in an infinite loop.

Arduino is built on top of C++ and FreeRTOS, There are mainly two IDEs: The official Arduino IDE, which uses the file extension `.ino`, and PlatformIO, which uses the file extension `.cpp`. The Arduino IDE is simpler, while PlatformIO is more powerful and supports other frameworks other than Arduino, such as STM32Cube, ESP-IDF, etc.


**Required Tools**
Before starting, some tools are required to be installed:
- PlatformIO: an open-source framework for embedded development. Just install the PlatformIO extension in VSCode, and it will handle the rest
- git, python, etc


**Debugging and Printing**

It'd hard to figure out the problem without setting up the debuging environment:
- Usb serial(USB CDC): the integrated serial within the debugger, like ST-Link for STM32, and ESP32's built-in debugger. This allows us to see the output of `Serial.println()` in the console.
- traditional debug interface: which allows us to set breakpoints, step through code, view variables, etc. 

online tutorials:
- [esp32 with platformio](https://randomnerdtutorials.com/vs-code-platformio-ide-esp32-esp8266-arduino/)

### Serial monitor for ESP32
ESP32 has a built-in USB CDC serial, so we don't need another USB to serial converter. 

First, some options need to be set in `platformio.ini`:
```ini
build_flags = 
  -DARDUINO_USB_CDC_ON_BOOT=1
  -DARDUINO_USB_MODE=1
```

In the code, we can use `Serial.println()` to print messages to the serial monitor. For example:
```cpp
void setup() {
    Serial.begin(115200);
    Serial.println("Hello, ESP32!");
}
void loop() {
    Serial.println("Looping...");
}
```

Then, we can use the built-in serial monitor in PlatformIO:
- command line: `pio device monitor`
- VSCode: click the "plug" icon in the bottom bar, platformio will automatically detect the serial port.
  

Notes and troubleshooting:
- if there are delays when opening the serial monitor, the message will be lost, and you won't see any output.   
- make sure you use the new version of the ESP32 Arduino core at [espressif32](https://github.com/platformio/platform-espressif32/releases)

## STM8 with Arduino
The STM8 microcontroller is a low-cost, 8-bit microcontroller, and running Arduino could be challenging, as only C is supported, rather than C++. The Arduino STM8 project is [sduino](https://github.com/tenbaht/sduino). It's based on SDCC, an open-source C compiler for STM8.

Quoted limitations of sduino:

    SDCC doesn't support C++. Some preprocessor magic is applied to close the gap between C and C++ syntax as much as possible, but this is not a 100% compatible drop-in replacement for full Arduino environments like for AVR or STM32


Examples for blinking, uart, etc can be found at 
- [platformio STM8 examples](https://github.com/platformio/platform-ststm8/tree/master/examples)
- [sduino examples](https://github.com/tenbaht/sduino/tree/development/examples)
- OLED, EEPROM,etc: [sduino API](https://tenbaht.github.io/sduino/api/Mini_SSD1306/)

## ESP32/STM32 with Arduino
ESP32 and STM32 are popular and powerful 32-bit microcontrollers, with good support for Arduino. 

ESP32 is popular for IoT applications with WIFI and Bluetooth, so a common use case is to build a web server on ESP32, where convenient libraries are provided for easy development with WIFI. 


A web server serving static files from SPIFFS: [ESP32 Web Server SPIFFS](https://randomnerdtutorials.com/esp32-web-server-spiffs-spi-flash-file-system/)

RTOS example: [ESP32 FreeRTOS](https://randomnerdtutorials.com/esp32-freertos-arduino-tasks/), it shows how to run multiple tasks in parallel via FreeRTOS, which is a real-time operating system for embedded devices.

## ESP32 with JVM or JavaScript
**ESP32 with JVM**
This requires FlintESPJVM, a JVM implementation for ESP32, providing hardware access like GPIO in Java. To start efficiently, we will use Scala and VsCode. The steps are as follows:
- create a new Scala sbt project, and add the sdk as a local library dependency.
- write code in Scala, by looking at the [Java examples]()
- run the command to compile and flash the code and FlintESPJVM to the ESP32 board.


**ESP32 with JavaScript**
To run JavaScript on ESP32, we can use Espruino, which is a JavaScript interpreter, as quoted from their website:

    Espruino is a JavaScript interpreter for microcontrollers. It is designed for devices with as little as 128kB Flash and 8kB RAM.

Espruino can be understood as a JavaScript version of Arduino, as it supports a wide range of microcontrollers, including STM32, ESP32, nrf series, etc.

We mainly focus on typescript and VSCode at (https://www.espruino.com/Typescript+and+Visual+Studio+Code+IDE), although the official Espruino IDE is provided. The [types for Espruino](https://www.npmjs.com/package/@types/espruino) can also be used by Scala.js.


A interesting feature in [FAQ](https://www.espruino.com/FAQ) is that `delay()` is discouraged, and call back functions in `setTimeout()` are preferred, which is common in software development, but not so common in embedded systems.

### Display
[OLED with SSD1306 driver](https://www.espruino.com/SSD1306)

## Debugging
Debugging embedded systems can be challenging due to the limited resources and lack of traditional debugging tools. common debugging methods include:
- Serial output: using `Serial.println()` to print debug messages to the serial monitor.
- LED indicators or LCD displays
- Debugging interfaces: using JTAG or SWD to connect to the microcontroller and use a debugger to set breakpoints, step through code, etc.
- Logic analyzers: to analyze the signals and communication between components.
- Emulators: using software emulators to simulate the embedded system and debug the code in a more traditional way.


common issues and troubleshooting:
- corrupted stack: this crashes the microcontroller, and it keeps restarting, and it's hard to debug, as no message can be printed after crashing. 

common pitfalls:
- writing to the same GPIO pin from multiple tasks. For example, one of ESP32's GPIO pins is connected to both an LED and a OLED display.