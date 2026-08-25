---
title: vibe coding keyboard
type: docs
---

The Ecofunctor VK1 is a small keyboard with a few keys, rotary encoders(knobs), and a small capacitive touch display. It is primarily designed for vibe coding(a coding paradigm that relies on probablistic large language models), but can also be used for other purposes as it is a standard HID keyboard, like for 3D modeling, video editing, etc. It features:
- 5 low profile mechanical keys
- 2 rotary encoders(knobs) with clicks suitable for forth and back like controls like previous/next, etc.
- 6 buttons on the touch display for sending predefined prompts or commands
- A small capacitive touch display for showing information like key mapping, system status, etc.
- Web UI to configure the key mapping, knob functions, sleep timer, etc.

## Usage
As a standard HID keyboard, each mechanical key and knob is mapped to function keys F13 to F24(to avoid conflict with standard keyboard keys). Specifically, the mapping is as follows:
- Key 1 to Key 5 are mapped to F13 to F17 respectively.
- The knob is mapped to F21 and F22 for clockwise and counter-clockwise rotation respectively.

In addition, the knob is also in charge of selecting the predefined prompts shown on the touch display. Once a prompt is selected, clicking the knob will send the prompt, just like manually typing the text. 

There are also extra buttons on the touch display for sending some common prompts as defined by the user. 


## Configuration
The keyboard is independent of software or IDE, whatever you use, like VSCode, Codex, as it's a generic Bluetooth keyboard, so it shall work with any software that can configure the key mapping/shortcuts.

The keyboard can be configured through a web UI. The user can define the key mapping, knob functions, sleep timer, and other settings. The web UI can be accessed by connecting the keyboard to a computer and opening the IP address of the keyboard in a web browser. 

To see the IP address of the keyboard, click the "Settings" button on the touch display. It will start a Wi-Fi hotspot. Connect to the hotspot and open the IP address shown on the touch display in a web browser. 


### recommended key mapping
The recommended key mapping for vibe coding is as follows, for keys
- 2 keys for keep or discard the current edit
- A key to open the chat dialog

knob functions:
- A knob for back and forth navigation for all agent/chat edits
- A knob for selecting the predefined prompts and clicking to send the prompt

buttons on the touch display:
- A button to extract the current selection into a new function
- A button to improve and optimize the codebase.

### Usage scenarios
Launch specific apps, like browsers, IDEs, or other software, can be done by installing some software in the computer, and then mapping the keys like F13 to F24 for the specific applications. 


## Internal Design
The keyboard is consists of:
- A microcontroller esp32-c3 with built-in Wi-Fi and Bluetooth
- A small capacitive touch display ST7789
- An IO expander PCF8574
- 5 kailh low profile mechanical switches
- 2 rotary encoders
- 2x 18650 batteries to provide 3.7V power supply.
- A 3D printed back case to hold all the components together. 
- Aluminum front case.


## changelog
v0.0: initial testing, prototype is built with jumpers, capative touch display, pcf8574 expander, and knobs work:
- testing module: esp32-c3 supermini
- focus on lvgl and touch display
- optimize the knob algorithm


v0.1: initial release, PCB is designed and manufactured, but LCD connection is wrong. 


v0.2: fixed the LCD connection, and everything works except wifi. io expander is upgraded to tca9535 with 16 GPIOs, as a test spot, so more native io can be used for battery level detection, and brightness control


v0.3: dump esp32-c3 supermini module for esp32-c3-wroom, and wifi issue is fixed. The 10k pull-up resistor for the i2c bus is not working. required changes:
- 4.7k pull-up resistors are needed for the i2c bus
- pull-up resistor needed for touch display wakeup.
- pcb size needs to be changed 
