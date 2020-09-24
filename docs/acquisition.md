---
title: Acquisition
parent: Generation 4
nav_order: 1
has_children: true
---

Here we describe what is needed to operate a Modular LED Display of the 4th generation. The first part concerns the knowledge necessary to make the decisions for hardware acquisition in the second part.

# Knowledge

You probably have a use case in mind when reading this. You can still learn about the initial motivation to develop modular LED Displays at ["Theory and Practice of Insect Flight Simulators."](../../../Generation 3/Software/docs/g2-user-guide.md)

## Parts overview

Fundamentally, G4 is about turning a light source on and off, possibly at different brightnesses and at well defined times. In the modular LED displays, the light source is a Light Emitting Diode (LED), which typically emit a well-defined spectrum of light. The G4 system combines 256 LEDs into a 16×16 matrix, which we call “Panel.” Each panel is a flat square measuring 40×40mm² (about 1.6×1.6 inches). Panels are organized in columns and arenas. A column consists of up to 4 panels that are directly connected, forming a maximum area of 160×40mm² with up to 1024 LEDs. Up to 12 columns can be combined into an "Arena." The arena is connected to a specialized PCIe IO card in a Windows computer through an interconnect board. Optionally, this IO card can also connect to a breakout box, which exposes some of the signals for recording. The "G4 Host" software on the computer interacts with the hardware and provides an API for the arena. User-friendly applications like the "Display Tools" can then be used to turn any of these 12,288 light sources on or off, up to 1500 times per second. The following paragraph gives more detail about what is necessary to address these more than 10,000 LEDs.

To understand the working principle in more detail, here a step through from the users' side: Using convenient tools like the Display Tools, you can define stimuli you wan to show. This description of the stimuli is sent to the "G4 Host", another application running in the computer background. When starting the G4 Host, this software automatically programs the specialized I/O card for high throughput and low latency communication with the arena. This PCIe card is a Field-Programmable Gate Array (FPGA) and is used by the G4 system to generate four different SPI communication channels. Once the G4 Host receives a command containing a stimuli description, the PCIe card sends these signals to the arena. The arena then splits the four SPI channels top the different columns. The columns consist of panels consisting of two separate boards: The communication board connected to the arena board and the adjacent panels, and the driver board with all the LEDs. The communication board has a microcontroller unit (MCU) that receives the incoming SPI signal, filtering for signals meant for this specific panel, and then forwards this signal to one of four connectors to the driver board. On the driver board, each of the connectors has its own MCU, which then translates the signal into corresponding on/off signals for the LEDs. The five MCUs per panel need to be preprogrammed before assembly to operate correctly. But we will come back to each of those points during the assembly.

## Capabilities

The G4 displays can show 16-bit stimuli with up to 500Hz and 1500Hz for purely turning them on and off. Different forms of arena boards can be used to place the 40×40mm² panels, each with 16×16 LEDs in columns up to 4 panels in height. An arena can drive up to 12 columns.

While the complexity and capability of the G4 displays have increased over previous generations, they are more accessible and easy to use through a set of advanced software tools. These "Display Tools" can be used to defined patterns and movements, arrange them into complex experimental protocols, and run data analysis on the results. These easy to use GUIs modify script which can be further customized by advanced users, should the experimental requirements go beyond what the current set of "Display Tools" supports.

## Difference to Generation 3

The main differences to the [Generation 3](/Generation 3) are the size of the panel (40×40mm² instead of 32×32mm² for G3). Within a panel area, the number of LEDs increased from 8×8 in G3 to 16×16 in G4. Consequently, G4 has an LED every 2.5mm at a higher density than the 4mm distance between LEDs in G3.

Technically, the displays now show synchronous controller driven updates, which means that patterns are only shown when the controller is sending data. 

This data transfer regime is possible since the communication between the controller and the panel changed to  Serial Peripheral Interface (SPI) from the previously used I²C in the previous generations.

The location of panels within the arena are defined by its position in the setup. Previous generations required that individual panels would be pre-programmed for a location within the setup. In G4, the address of each panel is defined by the column and the position within the column. Learn more details about this in the [subsection about placeholders](#placeholder).

# Hardware

Some parts of the G4 Modular LED Display needs to be produced, some can be bought. This website contains detailed information about the parts you need to produce and we provide example links to where you can buy the other parts. The picture below shows some examples for parts you can get.

![example parts](../assets/G4_hardware-overview.jpg)

## Produce

Producing PCBs takes time. A typical turn-around time for assemblers from the moment they receive the files to the moment you receive the hardware is one month. Over time and between manufacturers the production process differs. Manufacturers adjust the provided files, which sometimes means that the same set of files produce more or less reliable results between batches. If you are thinking about producing larger volume of either board, we strongly recommend running a smaller batch and thoroughly test that hardware. Once you have verified the results, order a larger volume from the same manufacturer. At each step of the process, try to get the files from the manufacturer that they used to produce your batch.

Please also let us know about your experiences and send us the files you sent to the manufacturers and the feedback you received from them. We have incorporated all previous feedback in the files we provide in our repositories to improve the quality of files. Over these iterations we hope to speed up the process and reduce possible errors and pitfalls in the design and the production of the hardware.



### Panel Driver PCB

### Arena PCB

### Arena Interconnect PCB

- G4 Panel boards consisting of
  - Driver PCB with LEDs
  - Communication PCB with connectors
- G4 Arena board
  - a full cylinder formed by 12 columns (the 12-12 board) or
  - a open cylinder where 12 of 18 possible columns are populated (the 12-18 board)
- Interconnect board
- Placeholder

## Buy

- Windows PC
- National Instruments PCIe-7842R PCI
- VHDCI cables
  - 1× SHC68-68-RDIO
  - 1× SHC68M-68F-RMIO
- National Instruments Breakout Box
- 5V Desktop power supply
  - depends on your setup, in most cases a [5V 10A like this one](https://www.adafruit.com/product/658) is OK

{::comment}TODO: add HARDWARE section. Maybe move parts from gs?{:/comment}
