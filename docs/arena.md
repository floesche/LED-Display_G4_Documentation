---
title: Arena
parent: Acquisition
grand_parent: Generation 4
nav_order: 7
---


# Arena Board

The arena board organized the panels in a geometry and provides structural integrity to the whole setup. Different shapes of cylindrical arenas have been built. They are often described by their number of panel columns populated and the virtual ones forming a full circle. A 12-12 arena is a closed cylinder formed by 12 columns in total. All of them can be populated in this design. A 12-18 arena is a cylinder that would be formed by 18 columns. Out of those, 12 can be populated. 

Here we share a 12-18 arena where the board occupies 299×206mm², designed as a PCB with 7 layers. The most stable production ready files are for [version v1.1](https://github.com/floesche/Arena-G4-Hardware/tree/master/arena_12-18/production_v1p1). There is also a version v2.0 being developed, but it is also more difficult and expensive to produce, since it uses hidden vias. The design was done in-house at Janelia.

## Arena Interconnect Board
{:#interconnect}

The 12-18 arena v1.1 has a ribbon cable input. An additional Arena Interconnect Board adapts the VHDI cable to the required ribbon cable format. This board is a simple 2 layer PCB within the dimensions of 4.9×8.4mm². The production files are available in [version v1.2](https://github.com/floesche/Arena-G4-Hardware/tree/master/interconnect/production_v1). The design was done in-house at Janelia. Recent tests suggest, that the ribbon cable introduces noise in the communication. The ribbon cable should be as short as possible to reduce the noise.