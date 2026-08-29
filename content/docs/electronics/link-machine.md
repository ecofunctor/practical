---
title: Linking machine
type: docs
---

The linking machine is named generically, as it aims to help people memorize, thus linking the knowledge together. 

For English learning, it aims at advanced learners, who already have a basic vocabulary, since the user interface is purely English, without any Chinese or other languages for translation or hints. 

Physically, the linking machine is a small device with a eye friendly display, like reflective monochrome LCD, or E-ink, with capacitive touch screen, and a few knobs and buttons for navigation. 

## physical design
Main components in PCB:
- mcu: esp32s3-wroom, and optional place for esp32-c3-wroom
- display: 4.2 inch monochrome LCD with touch screen
- storage: soldered flash and sdcard slot
- input: a knob, 2 buttons
- audio: output for earphone and speakers, and mic
- power: usb-c for charging and power supply, and battery
- extension: unused io pins are exposed via headers like 1.0mm/1.27mm pitch, and a few test points for debugging and flashing


# English learning
For vocabulary building, the linking machine is mainly built on the idea of wordnet, which is a graph of words, where each word is a node, and the edges connect the words with their synonyms, antonyms, and other relations. 

Vocabulary building features:
- phonics: showing the phonics of the word
- synonyms and antonyms
- example sentences, and words in the sentences are also clickable.
- wordnet: showing the wordnet of the word as the main view. it has 155,327 words.

# Mathematics
The mathematics part is still under development. Initial ideas are discussed below. 


For mathematics, the linking machine may also uses the idea of graph, where each node is a mathematical concept, but the crucial part is to organize the concepts in a way that is far apart from the traditional way of teaching mathematics:
- equations
- functions
- operations: addition, subtraction, multiplication, division, exponentiation
- expressions: polynomials, rational expressions, trigonometric expressions, etc.

# Other software
The machine/tablet is open source, so users can flash whatever they want, like the Tac
or use it like a development board, as it has exposed IO pins and a not too small touch screen, making it suitable for:
- information display
- control panel for other devices
- (quasi) portable computer, like m5stack
- retro style electronics like PDA, electronic dictionary, etc.
