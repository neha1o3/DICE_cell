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
- [Author](#author)
- [Acknowledgements](#acknowledgements)
- [References](#references)

## Introduction 
   Exposure to radiation environments brings great challenges to integrated circuits designers. A single event upset (SEU) is an error induced by an incident particle on an integrated circuit. The incident particle generates electron hole pairs as it traverses through the semiconductor material. The electrons (or holes) may get collected at a circuit node, resulting in a voltage perturbation at that node. Such a transient then may propagate through the circuit connected to the affected node and may introduce operational errors. If the affected node belongs to a latch design, the data stored in the latch may get altered, resulting in an SEU. 
- Design hardening techniques at circuit level can be developed to achieve immunity to upsets. Because of superior SEU performance and acceptable performance penalties possible, DICE-based designs are preferred over all other latch designs.
## Working
The upset immune storage cell design, which uses a novel 4-node redundant structure, is shown in Fig. 1. 
![image](https://user-images.githubusercontent.com/100678578/156162424-184fc084-ffe1-4c08-8bfb-03d8fcc4209d.png)

Fig. 1. The DICE Memory Cell

The four nodes Xo...X3 store the data as two pairs of complementary values (i.e., 1010 or 0101) which are simultaneously accessed using transmission gates for write or read operation. Two opposite feedback loops are formed, one is the P-transistor loop, P0…P3 other is N- transistor loop, N3…N0. If we consider logic state 0 as X0…X3=0101, then N0, P1, N2 and P3 are in conduction., blocking the other transistors, and storing the same data. For logic state 1, X0…X3=1010, N1, P2, N3 and P0 are in conduction, performing the latch function in similar manner. 

Proof: A negative upset pulse at a node 𝑋i(i=0…3) will induce a positive pulse perturbation at node 𝑋(i+1) through transistor P(i+1). But this will not be able to affect logic stored at 𝑋(i-1) since 𝑁(i-1) is blocked by the negative upset pulse. Hence the positive perturbation at node 𝑋(i+1) is not further transmitted. This perturbation is removed after the upset transient, restoring the correct logic state. A similar analysis can be done for positive transient upset pulse. This shows that whatever electrical charge collected at the perturbed node, the cell recovers its initial state. 
## Reference Circuit
## Author
[Neha Sharma](https://www.linkedin.com/in/neha-sharma-7b19531b7), B.Tech(EE), Indian Institute of Technology Jammu, Jammu, India
-  Contact: [nesharma1003@gmail.com](nesharma1003@gmail.com)
## Acknowledgements
- [Cloud Based Analog IC Design Hackathon](https://hackathoniith.in/)
- [Synopsys India](https://www.synopsys.com/)
- [VLSI System Design (VSD) Corp. Pvt. Ltd India](https://www.vlsisystemdesign.com/)
## References
- [T. Calin, M. Nicolaidis, and R. Velazco, “Upset hardened memory design for submicron CMOS technology,” IEEE Trans. Nucl. Sci., vol. 43, no. 6, pp. 2874–2878, Dec. 1996.](https://ieeexplore.ieee.org/document/556880)
- [H. . -B. Wang et al., "An SEU-Tolerant DICE Latch Design With Feedback Transistors," in IEEE Transactions on Nuclear Science, vol. 62, no. 2, pp. 548-554, April 2015](https://ieeexplore.ieee.org/document/7052424)
