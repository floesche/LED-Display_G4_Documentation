---
title: Components
parent: Development
grand_parent: Generation 4
nav_order: 1
---

1. TOC
{:toc}


# System Components

The prototype G4 system consists of four components:

- Display panels - 20 display panels, each panel has a four 8x8 20mm LED matrices.
- Test Arena - configurable planar arena which can accommodate 6 columns of panels.  
- Demo Controller - simple Arduino Uno based controller which shows a moving stripe pattern.
- 5V power supply (2.1mm center positive).

![](../assets/coleman_bundle.png)


A fork of the repository with design files for G4 panels hardware can be found [here](https://github.com/floesche/panels_g4_hardware). Note, the design files for the PCBs use the [kicad EDA](https://kicad-pcb.org/) software suite.

A fork of the source code for the firmware used by the display panels and the demo controller can be found [here](https://github.com/floesche/panels_g4_firmware). 

# Display Panels

A display panel consists of two sub-panel PCBs - the comm (communications) sub-panel and  the driver (display) sub-panel. 

![Display panels](../assets/display_panels.png)

## Driver Sub-Panels

The driver sub-panel has four atmega328 micro-controllers - one for each 8x8
display matrix. Each micro-controller on the driver sub-panel is responsible
for receiving pattern data from the comm sub-panel over I2C and displaying this
data on its associated LED matrix. The four LED matrices which attach
to the driver are ordered from  0 to 3 as shown in the image below. 


![driver sub-panel](../assets/atmega_driver_front.png)

[download PCB Schematic](../assets/driver.pdf)

## Comm Sub-Panels

The comm sub-panel contains a single atmega328 micro-controller which
communicates with the display controller over SPI. The comm sub-panel's sole
resposibility is to receive pattern data from the controller (via SPI) and
send it on to the driver sub-panel (via I2C). 

![Comm sub-panel](../assets/atmega_comm_front.png)

[download PCB Schematic](../assets/comm.pdf)

# Test Arena 

The test arena is used to connect the panels with the controller and to supply
power to the panels. There are three headers which can be used to connect the
panels to the display controller.  

- P22 40-Pin (2x20) single SPI bus header. 
- P23 60_Pin (2x30) six SPI bus header.
- P30 40-Pin (2x20) six SPI bus w/ common chip select lines.

![Test arena](../assets/test_arena.png)

5V power is supplied to the panels via 2.1mm DC jack, polarity is center positive. 

There are 5 sets of jumpers which can be used to configure the arena.  (**TODO**: document jumper functions - for now refer to the arena schematic.)

[download Arena PCB Schematic](../assets/arena.pdf)

# Demo Controller

A demonstration controller, based on an Arduino Uno, is provided with the arena
and panels.  The demonstration controller connects to header P22 on the arena and will
display a moving stripe pattern in 16-level gray scale mode.  The panels (up to
four) should be connected to header P1 when using the demo controller. 
Note, the demo controller requires 5V power via the USB connector on the
Arduino Uno in order to operate.

![Demo controller](../assets/demo_controller.png)

A video of the demo controller connected to the test arena and displaying the moving stripe pattern is shown below. 

# 5V Power Supply

A 5V 1A power supply is provided with the prototype panels, arena and
controller. This supply is sufficient for operating roughly four panels - so
enough for running the demo controller.  A higher current supply will likely be
required in order to operate more than four panels. When selecting a power
supply roughly 0.25A should be budgeted for each panel.  The connector is a
2.1mm DC jack and the supply should be center positive.
