# Transistor-Level 8-Bit Calculator

A physical 8-bit binary arithmetic calculator engineered entirely from discrete passive and active components, operating with zero integrated circuit chips.

[![Hardware](https://img.shields.io/badge/Hardware-Discrete%20BJTs%20%26%20Resistors-red.svg)](#circuit-architecture)
[![Logic](https://img.shields.io/badge/Logic-Pure%20NAND%20Synthesis-blue.svg)](#nand-logic-synthesis)
[![Layers](https://img.shields.io/badge/Form%20Factor-7%20Stacked%20Breadboards-purple.svg)](#physical-layout)

---

## 1. Project Overview

Modern microprocessors abstract arithmetic behind billions of microscopic transistors on monolithic silicon dies. The goal of this project was to demystify digital computation by engineering a fully functional **8-bit binary adder directly at the silicon junction level**, using individual BJT transistors wired into fundamental NAND gates across seven stacked prototype breadboard layers.

- **Arithmetic Operation**: 8-bit parallel binary addition ($0 + 0$ to $255 + 255$, output range $0 - 510$ with 9-bit carry).
- **Core Component Count**: 63 discrete NPN BJT transistors, 190+ precision resistors, discrete LEDs, and zero integrated circuits (0 ICs).
- **Physical Construction**: Multi-tier vertical interconnect stack minimizing parasitic trace capacitance and routing congestion.

---

## 2. Circuit Architecture & NAND Synthesis

All boolean logic functions (AND, OR, XOR, NOT) are synthesized strictly using **NAND logic gates**, built from discrete bipolar junction transistors operating in saturation and cutoff modes.

### Discrete BJT NAND Gate Topology
Each NAND gate is constructed using:
- Two NPN transistors in series (cascode pull-down network).
- Base pull-up resistors for switching thresholds.
- Collector pull-up resistor establishing logic HIGH ($V_{CC} = 5\text{V}$) when either input is LOW, and logic LOW ($V_{CE(sat)} \approx 0.2\text{V}$) when both inputs are saturated HIGH.

### Full-Adder Synthesis from NAND Logic
For each bit slice $i$ ($i = 0 \dots 7$):
- **Inputs**: $A_i, B_i, C_{in}$
- **Outputs**: Sum $S_i$, Carry Out $C_{out}$
- **NAND Gate Count**: 9 NAND gates per full adder bit:
  $$\text{Half Adder 1: } 4 \text{ NAND gates} \implies S_1 = A \oplus B, \; C_1 = A \cdot B$$
  $$\text{Half Adder 2: } 4 \text{ NAND gates} \implies S_i = S_1 \oplus C_{in}, \; C_2 = S_1 \cdot C_{in}$$
  $$\text{Carry Merge: } 1 \text{ NAND gate} \implies C_{out} = C_1 + C_2$$

---

## 3. Physical Layout & Multi-Tier Routing

Constructing 63 transistors and 190+ resistors on a single breadboard introduces severe wire congestion and signal degradation. To solve this:
1. **7 Stacked Prototype Layers**: The circuit is segmented vertically into dedicated bit-slice modules.
2. **Carry-Chain Interconnects**: Inter-layer jumper headers route the critical carry signal ($C_0 \to C_7$) vertically between breadboard planes.
3. **Decoupled Power Rails**: Distributed power bus routing ensures stable collector current during high-frequency switching transients.
4. **Visual Telemetry**: Discrete high-efficiency LEDs on each bit slice display the real-time binary state of the sum register and the overflow carry bit.

---

## 4. Hardware Specifications

| Parameter | Specification |
| :--- | :--- |
| **Data Width** | 8-Bit Binary ($A_7\dots A_0 + B_7\dots B_0$) |
| **Max Decimal Sum** | $510$ ($11111111_2 + 11111111_2 = 111111110_2$) |
| **Active Components** | 63 Discrete NPN BJT Transistors (2N3904 / 2N2222) |
| **Passive Components** | 190+ Metal Film Resistors |
| **Integrated Circuits** | **0** (No 74xx series chips, no microcontrollers, no ICs) |
| **Operating Voltage** | 5.0 V DC regulated supply |
| **Form Factor** | 7 Stacked Solderless Prototype Breadboard Layers |
| **Indicators** | 8× Sum Bit LEDs + 1× Carry-Out Overflow LED |

---

## 5. Repository Contents

This repository documents the circuit schematics, transistor-level NAND topology, component bill of materials (BOM), and mechanical stack diagrams for the physical 8-bit calculator.

---

## Author

**Mohammad Safi** — Electrical Engineering, University of Houston.  
Specializing in embedded systems, digital design, and machine learning.

- **Portfolio**: [thmfirst50-jpg.github.io](https://thmfirst50-jpg.github.io/)
- **LinkedIn**: [linkedin.com/in/safi0](https://linkedin.com/in/safi0/)
