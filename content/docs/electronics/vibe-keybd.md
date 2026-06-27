---
title: vibe coding keyboard
type: docs
---

The Ecofunctor VK1 is a small keyboard with a few keys, rotary encoders(knobs), and a small capacitive touch display. It is primarily designed for vibe coding(a coding paradigm that relies on probablistic large language models), but can also be used for other purposes as it is a standard HID keyboard, like for 3D modeling, video editing, etc. It features:
- 8 low profile mechanical keys
- 2 rotary encoders(knobs) suitable for forth and back like controls like previous/next, etc.
- A small capacitive touch display for showing information like key mapping, system status, etc.
- Web UI to configure the key mapping, knob functions, sleep timer, etc.

## Usage
As a standard HID keyboard, each mechanical key and knob is mapped to function keys F13 to F24(to avoid conflict with standard keyboard keys). Specifically, the mapping is as follows:
- Key 1 to Key 8 are mapped to F13 to F20 respectively.
- The knob is mapped to F21 and F22 for clockwise and counter-clockwise rotation respectively.

In addition, the knob is also in charge of selecting the predefined prompts shown on the touch display. Once a prompt is selected, clicking the knob will send the prompt, just like manually typing the text. 

There are also extra buttons on the touch display for sending some common prompts as defined by the user. 


## Configuration
The keyboard can be configured through a web UI. The user can define the key mapping, knob functions, sleep timer, and other settings. The web UI can be accessed by connecting the keyboard to a computer and opening the IP address of the keyboard in a web browser. 

To see the IP address of the keyboard, click the "Settings" button on the touch display. It will start a Wi-Fi hotspot. Connect to the hotspot and open the IP address shown on the touch display in a web browser. 

## Internal Design
The keyboard is consists of:
- A microcontroller esp32-c3 with built-in Wi-Fi and Bluetooth
- A small capacitive touch display ST7789
- An IO expander PCF8574
- 8 kailh low profile mechanical switches
- 2 rotary encoders
- 2x 18650 batteries to provide 3.7V power supply.
- A 3D printed back case to hold all the components together. 
- Aluminum front case.
