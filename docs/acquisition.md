---
title: Aquisition
parent: Generation 4
nav_order: 1
---

Here we describe what is needed to operate a Modular LED Display of the 4th generation. The first part concerns knowledge that is needed to make the decisions for hardware acquisition in the second part.

# Knowledge

You probably have an use case in mind when reading this, but you can learn about the initial motivation to develop modular LED Displays at ["Theory and Practice of Insect Flight Simulators"](../../../Generation 3/Software/docs/g2-user-guide.md).

## Parts overview

Fundamentally, G4 is about turning a light source on and off, possibly at different brightnesses and at well defined times. In the case of the modular LED displays, the light source is an Light Emitting Diode (LED) which typically emit a well defined spectrum of light. For the G4 system, 256 LEDs are combined into a 16×16 matrix which we call "Panel". Each panel is a flat square measuring 40×40mm² (about 1.6×1.6 inch). Panels are organized in columns and arenas. A columns consists of up to 4 panels that are directly connected to each other forming a maximum area of 160×40mm² with up to 1024 LEDs. Up to 12 columns can be combined into an "Arena". Through an interconnect board, the arena is connected to a specialized PCIe IO card in a Windows computer. Optionally, this IO card can also be connected to a breakout box. The "G4 Host" software on the computer interacts with the hardware and provides an API for the arena. User friendly applications like the "Display Tools" can then be used, to turn any of these 12,288 light sources on or off, up to 1500 times per second. The following paragraph gives more detail about what is necessary to address these more then 10,000 LEDs.

To understand the working principle in more detail, here a step through from the users side: Using convenient tools like the Display Tools, you can define stimuli you wan to show. This description of the stimuli is sent to the "G4 Host", another application running in the background of the computer. When starting the G4 Host, this software automatically programms the specialized I/O card for high throughput and low latency communication with the arena. Basically, this PCIe card is a Field-Programmable Gate Array (FPGA) and is used by the G4 system to generate four different SPI communication channels. Once the G4 Host receives a command containing a stimuli description, the PCIe card sends these signals to the arena. The arena then splits the four SPI channels top the different columns. The columns consist of panels which itself consist of two different boards: The communication board that is connected to the arena board and to the neighboring panels, and the driver board that has all the LEDs. The communication board has a microcontroller unit (MCU) which receives the incoming SPI signal, decides which signals are meant for this specific panel, and then forwards this signal to one of four connectors to the driver board. On the driver board, each of the connectors has its own MCU which then translates the signal into corresponding on/off signals for the LEDs. The five MCUs per panel need to be preprogrammed before assembly to operate correctly. But we will come back to each of those points during the assembly.


## Capabilities

The G4 displays are capable of showing 16 bit stimuli with up to 500Hz for 16-level brightness scale and 1500Hz on a 2-level brightness scale. Different forms of arena boards can be used to place the 40×40mm² panels each with 16×16 LEDs in columns up to 4 panels in height. An arena can drive up to 12 columns.

While the complexity and capability of the G4 displays has increased over previous generations, they are more accessible and easy to use through a set of advanced software tools. These "Display Tools" can be used to defined patterns and movements, arrange them into complex experimental protocols, and run data analysis on the results. These easy to use GUIs modify script which can be further customized by advanced users, should the experimental requirements go beyond what the current set of "Display Tools" supports.


## Difference to Generation 3

The main differences to the [Generation 3](/Generation 3) are the size of the panel (40×40mm² instead of 32×32mm² for G3), the use of Serial Peripheral Interface (SPI) instead of I²C, and synchronous controller driven updates, which means that patterns are only shown when the controller is sending data.


{::comment}TODO: add HARDWARE section. Maybe move parts from gs?{:/comment}
