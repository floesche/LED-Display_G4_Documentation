---
title: Commodity items
parent: Acquisition
grand_parent: Generation 4
nav_order: 9
---

# Computer

Once the hardware is put together, the arena is going to be controlled from a dedicated computer. Two applications, namely MATLAB and a Simulink based custom application, need to run in parallel on this machine. The faster this machine the better, but we cannot give a recommendation on what the lower limit is. Most recently we used Dell Precision 5820 Workstations, but other recent PC with a PCIe slot will most likely work, too. 

# Multi I/O card

This machine will need to have a National Instruments Multifunction Reconfigurable I/O device, specifically the PCIe-7842, installed. Note that the card does not always work in all PCIe slots. In our test systems, the card worked in 2 out of 5 slots.

# Arduino Uno

The programmer is currently built around an Arduino Uno. The are widely available, for example at [1](https://store.arduino.cc/usa/arduino-uno-rev3) and [2](https://www.digikey.com/short/zr4nd5).

# Power supply

In the past we have had no problems with 5V 10A power supplies such as [this one](https://www.adafruit.com/product/658). Here is why this should be OK:

Depending on the choices on LEDs and resistors you made during the acquisition of the driver boards, a single LED typically draws between 10 and 20mA when turned on. Because of the line scan algorithm, not more than 8 LEDs per quadrant are powered on at any time, so not more than 32 per panel. Since we use up to 4 different SPI busses, up to 128 LEDs can be turned on at the same time. This amounts to less than 3A for the light.

With 5 ATMega328 per panel and 48 panels, up to 240 ATmega328 need to be powered all the time. Assuming another 20mA per MCU, this amounts to roughly 5A.

# VHDCI cable(s)

For the connection between PCIe card and interconnect board, you will need one [SHC68-68-RDIO](https://www.ni.com/en-us/shop/accessories/products/digital-cable.html?skuId=30215) cable. For the connection between the PCIe card and the breakout box a [SHC68M-68F-RMIO](https://www.ni.com/en-us/support/model.shc68m-68f-rmio-cable.html) cable was recommended. Both use the same connector, but we could only get reliable results when using the cables in the described way.

{::comment}
TODO: find out which breakout box exactly
# NI Breakout box
{:/comment}

