## Introduction

This project is centered around the design and implementation of a **4-bit Hybrid Arithmetic Logic Unit (ALU)** using a **hierarchical approach** in Verilog. The main goal is to demonstrate a complete **ASIC RTL-to-GDSII design flow**, incorporating both custom macro design and top-level integration.

###  Key Objectives

-  **Design a Modular ALU**  
  Create a 4-bit ALU using a clean, hierarchical structure by reusing a custom-designed `full_adder` module.

- **Custom Macro Implementation**  
  Synthesize, place & route, and characterize the `full_adder` separately. Generate its `.lib` using PrimeTime and `.db` using Library Compiler.

- **Top-Level ALU Integration**  
  Integrate the soft macro into the `hybrid_alu` module, which performs multiple arithmetic and logical operations based on a 3-bit control signal.

  # Full Digital VLSI Flow Using Synopsys Tools
  
  -  **Design Compiler (DC)** – Used to convert Verilog RTL code into a gate-level netlist (logic synthesis).  
  -  **IC Compiler II (ICC2)** – Used to create the physical layout of the design (placement, routing, and GDSII generation).  
  -  **PrimeTime** – Used to analyze timing and create a `.lib` file (characterizing the delay, area, and power of the full_adder macro).  
  -  **Library Compiler (LC)** – Converts the `.lib` file into a `.db` format, which is required by synthesis tools like DC.
