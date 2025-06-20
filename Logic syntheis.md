# What is Synthesis?
Synthesis is the process of converting your RTL design (written in Verilog or VHDL) into a gate-level netlist made of real logic gates (AND, OR, Flip-Flops, MUX, etc.) using a specific technology library.

It prepares your design for physical implementation (like floorplanning and routing in IC Compiler).

## Inputs to Synthesis

| Input                          | Description                                                                  |
| ------------------------------ | ---------------------------------------------------------------------------- |
| **RTL Code**                   | Verilog/VHDL files describing your digital logic (e.g., `full_adder.v`)      |
| **Technology Library** (`.db`) | Contains info about available gates, delays, area, etc. Used for mapping RTL |
| **Constraints File** (`.sdc`)  | Defines clocks, input/output delays, timing exceptions 


## Outputs from Synthesis

| Output                                | Description                                                |
| ------------------------------------- | ---------------------------------------------------------- |
| **Gate-Level Netlist** (`.v`, `.ddc`) | Mapped to actual standard cells. Used for physical design. |
| **Reports**                           | Area, timing, power reports (`.rpt` files)                 |
| **Constraint-Checked Design**         | Includes checks for setup, hold, and clock constraints     |



#  Hybrid ALU – Logic Synthesis Report

The logic synthesis stage of a hierarchical ALU implemented using Verilog and synthesized using Synopsys Design Compiler (DC). The ALU is composed of reusable `full_adder` blocks performing `add`, `sub`, `inc`, and `dec` operations.

## Tool Used
- Tool: Synopsys Design Compiler 

- Target Library: saed32rvt_tt0p78vn40c.db

- Custom Block Library: fulladder.db

- Technology Node: 32nm (SAED32)


![Screenshot from 2025-06-19 13-52-41](https://github.com/user-attachments/assets/5ac27c53-a349-40d1-8eff-8728ec4c9db4)


