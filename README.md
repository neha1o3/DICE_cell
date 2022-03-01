# Dual Interlocked Storage Cell
This repository presents the design of transmission gate latch circuit and clocked inverter latch circuit using the DICE (Dual Interlocked Storgae Cell). These designs are implemented on Synopsys Custom Compiler in 28nm technology node.
## Table of Contents 
- [Introduction](#introduction)
- [Working](#working)
- [Reference_Circuit](#reference_circuit)
- [Implementation](#implementation)
- [Schematic_Netlist_Waveform](#schematic_netlist_waveform)
- [Methodology](#methodology)
- [Netlist](#netlist)
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
![image](https://user-images.githubusercontent.com/100678578/156172125-9f22c027-d5a7-4e17-94ee-fba826614d42.png)

![image](https://user-images.githubusercontent.com/100678578/156171366-cdad20dd-dcb1-4ded-b238-082bab16a87d.png)

## Netlist
The netlist of the Transmission Gate Latch Circuit using DICE cell is as follows.
```*  Generated for: PrimeSim
*  Design library name: neha_lib1
*  Design cell name: neha_tb
*  Design view name: schematic
.lib 'saed32nm.lib' TT

*Custom Compiler Version S-2021.09
*Tue Mar  1 12:50:23 2022

.global gnd!
********************************************************************************
* Library          : neha_lib1
* Cell             : neha_inv
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
.subckt neha_inv ck d q qb
xm3 net29 net25 net41 net41 p105 w=0.1u l=0.03u nf=1 m=1
xm2 net25 qb net41 net41 p105 w=0.1u l=0.03u nf=1 m=1
xm1 qb q net41 net41 p105 w=0.1u l=0.03u nf=1 m=1
xm0 q net29 net41 net41 p105 w=0.1u l=0.03u nf=1 m=1
xn5 d ck net25 gnd! n105 w=0.1u l=0.03u nf=1 m=1
xn4 d ck q gnd! n105 w=0.1u l=0.03u nf=1 m=1
xn3 net29 q gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xn2 net25 net29 gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xn1 qb net25 gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xn0 q qb gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
v8 net41 gnd! dc=1
.ends neha_inv

********************************************************************************
* Library          : neha_lib1
* Cell             : neha_tb
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
xi0 clk d q q_bar neha_inv
v2 d gnd! dc=0 pulse ( 0 1 0 0.01u 0.01u 2u 4u )
v1 clk gnd! dc=0 pulse ( 0 1 0 0.01u 0.01u 1.2u 2.4u )
c5 q gnd! c=1p
c4 q_bar gnd! c=1p








.tran '1u' '20u' name=tran

.option primesim_remove_probe_prefix = 0
.probe v(*) i(*) level=1
.probe tran v(clk) v(d) v(q) v(q_bar)

.temp 25



.option primesim_output=wdf


.option parhier = LOCAL






.end
```
The netlist of the Clocked Inverter Latch Circuit using DICE cell can be seen below.
```*  Generated for: PrimeSim
*  Design library name: neha_lib1
*  Design cell name: inv_tb
*  Design view name: schematic
.lib 'saed32nm.lib' TT

*Custom Compiler Version S-2021.09
*Tue Mar  1 12:33:31 2022

.global gnd!
********************************************************************************
* Library          : neha_lib1
* Cell             : clk_inv
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
.subckt clk_inv d q q_bar clk clk_bar
xp5 q_bar clk_bar net57 net76 p105 w=0.1u l=0.03u nf=1 m=1
xp4 net57 d net76 net76 p105 w=0.1u l=0.03u nf=1 m=1
xp6 net71 clk_bar net57 net76 p105 w=0.1u l=0.03u nf=1 m=1
xp3 net45 q_bar net76 net76 p105 w=0.1u l=0.03u nf=1 m=1
xp8 q_bar clk net17 net76 p105 w=0.1u l=0.03u nf=1 m=1
xp2 net17 q net76 net76 p105 w=0.1u l=0.03u nf=1 m=1
xp7 net71 clk net3 net76 p105 w=0.1u l=0.03u nf=1 m=1
xp1 q net71 net76 net76 p105 w=0.1u l=0.03u nf=1 m=1
xp0 net3 net45 net76 net76 p105 w=0.1u l=0.03u nf=1 m=1
xn6 net71 clk net67 gnd! n105 w=0.1u l=0.03u nf=1 m=1
xn4 net67 d gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xn5 q_bar clk net67 gnd! n105 w=0.1u l=0.03u nf=1 m=1
xn3 net45 net71 gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xn2 net41 net45 gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xn8 q_bar clk_bar net41 gnd! n105 w=0.1u l=0.03u nf=1 m=1
xn0 net33 q gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xn7 net71 clk_bar net33 gnd! n105 w=0.1u l=0.03u nf=1 m=1
xn1 q q_bar gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
v9 net76 gnd! dc=1
.ends clk_inv

********************************************************************************
* Library          : neha_lib1
* Cell             : inv_tb
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
xi0 d q q_bar clk clk_bar clk_inv
v3 clk gnd! dc=0 pulse ( 0 1 0 0.01u 0.01u 1.2u 2.4u )
v2 d gnd! dc=0 pulse ( 0 1 0 0.01u 0.01u 2u 4u )
c6 q gnd! c=1p
c4 q_bar gnd! c=1p
xm9 clk_bar clk net24 net24 p105 w=0.1u l=0.03u nf=1 m=1
xm10 clk_bar clk gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
v11 net24 gnd! dc=1








.tran '1u' '20u' name=tran

.option primesim_remove_probe_prefix = 0
.probe v(*) i(*) level=1
.probe tran v(clk) v(clk_bar) v(d) v(q) v(q_bar)

.temp 25



.option primesim_output=wdf


.option parhier = LOCAL






.end
```

## Author
[Neha Sharma](https://www.linkedin.com/in/neha-sharma-7b19531b7), B.Tech(EE), Indian Institute of Technology Jammu, Jammu, India
-  Contact: nesharma1003@gmail.com
## Acknowledgements
- [Cloud Based Analog IC Design Hackathon](https://hackathoniith.in/)
- [Synopsys India](https://www.synopsys.com/)
- [VLSI System Design (VSD) Corp. Pvt. Ltd India](https://www.vlsisystemdesign.com/)
## References
- [T. Calin, M. Nicolaidis, and R. Velazco, “Upset hardened memory design for submicron CMOS technology,” IEEE Trans. Nucl. Sci., vol. 43, no. 6, pp. 2874–2878, Dec. 1996.](https://ieeexplore.ieee.org/document/556880)
- [H. . -B. Wang et al., "An SEU-Tolerant DICE Latch Design With Feedback Transistors," in IEEE Transactions on Nuclear Science, vol. 62, no. 2, pp. 548-554, April 2015](https://ieeexplore.ieee.org/document/7052424)
