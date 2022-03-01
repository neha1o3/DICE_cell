# Dual Interlocked Storage Cell
This repository presents the design of transmission gate latch circuit and clocked inverter latch circuit using the DICE (Dual Interlocked Storgae Cell). These designs are implemented on Synopsys Custom Compiler in 28nm technology node.
## Table of Contents 
- [Introduction](#introduction)
- [Working](#working)
- [Reference_Circuit](#reference_circuit)
- [Implementation](#implementation)
- [Schematic_Netlist_Waveform](#schematic_netlist_waveform)
- [Methodology](#methodology)
- [Challenge](#challenge)
- [Troubleshooting](#troubleshooting)
- [Reproduce_waveforms](#reproduce_waveforms)
- [Limitations](#limitations)
- [References](#references)
- [Acknowledgements](#acknowledgements)
- [Author](#author)
## Introduction 
   Exposure to radiation environments brings great challenges to integrated circuits designers. A single event upset (SEU) is an error induced by an incident particle on an integrated circuit. The incident particle generates electron hole pairs as it traverses through the semiconductor material. The electrons (or holes) may get collected at a circuit node, resulting in a voltage perturbation at that node. Such a transient then may propagate through the circuit connected to the affected node and may introduce operational errors. If the affected node belongs to a latch design, the data stored in the latch may get altered, resulting in an SEU. 
- Design hardening techniques at circuit level can be developed to achieve immunity to upsets. Because of superior SEU performance and acceptable performance penalties possible, DICE-based designs are preferred over all other latch designs.
## Working
The upset immune storage cell design, which uses a novel 4-node redundant structure, is shown in Fig. 1. 
![image](https://user-images.githubusercontent.com/100678578/156162424-184fc084-ffe1-4c08-8bfb-03d8fcc4209d.png)

Fig. 1. The DICE Memory Cell

The four nodes Xo...X3 store the data as two pairs of complementary values (i.e., 1010 or 0101) which are simultaneously accessed using transmission gates for write or read operation. Two opposite feedback loops are formed, one is the P-transistor loop, P0…P3 other is N- transistor loop, N3…N0. If we consider logic state 0 as X0…X3=0101, then N0, P1, N2 and P3 are in conduction., blocking the other transistors, and storing the same data. For logic state 1, X0…X3=1010, N1, P2, N3 and P0 are in conduction, performing the latch function in similar manner. 
