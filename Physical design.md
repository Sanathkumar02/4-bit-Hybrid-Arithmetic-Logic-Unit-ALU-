# Floorplanning

- This stage involves defining the physical structure of the synthesized hierarchical ALU by allocating space, creating rows, and placing macros using Synopsys IC Compiler II (ICC2)
- The floorplan was created after synthesis and netlist import.

- Each ALU sub-module (add, subtract, increment, decrement) is built using the full_adder macro.

  <img width="674" alt="Screenshot 2025-06-10 181136" src="https://github.com/user-attachments/assets/31ff772c-779e-4235-b752-4e143964e520" />

 
 
 Floorplan view of the hierarchical ALU design with 4 sub-modules (FA_add, FA_sub, FA_inc, FA_dec) using full_adder macros.
