# Floorplanning

- This stage involves defining the physical structure of the synthesized hierarchical ALU by allocating space, creating rows, and placing macros using Synopsys IC Compiler II (ICC2)
- The floorplan was created after synthesis and netlist import.

- Each ALU sub-module (add, subtract, increment, decrement) is built using the full_adder macro.

  <img width="674" alt="Screenshot 2025-06-10 181136" src="https://github.com/user-attachments/assets/31ff772c-779e-4235-b752-4e143964e520" />

 
 
 Floorplan view of the hierarchical ALU design with 4 sub-modules (FA_add, FA_sub, FA_inc, FA_dec) using full_adder macros.





# Macro Placement

- The ALU design consists of four macro blocks:
   - FA_inc, FA_dec, FA_sub, and FA_add

- Each macro is an instance of the reusable block full_adder synthesized into fulladder.db.

- The macros were placed manually for better spatial organization and easier routing.

- Manual placement ensures:

   - Predictable routing paths

   - Improved control over congestion

   - Better utilization of core area
 
     
![Screenshot from 2025-06-19 14-47-36](https://github.com/user-attachments/assets/36e501a5-9260-42ea-89f8-300111e0a445)


# Keepout Margins
- A keepout margin was applied around each macro using ICC2’s GUI features.

- Purpose of keepout margins:

   -Prevents standard cell placement too close to the macros

   - Avoids routing congestion near macro edges

   - Ensures clean spacing for power/ground rails and signal routes


![Screenshot from 2025-06-19 14-21-35](https://github.com/user-attachments/assets/27555308-cbbc-4858-858c-6769bcf8eed4)



 # POWERPLANNIG


Power planning is the process of designing a robust power distribution network (PDN) in an integrated circuit (IC) layout to deliver power (VDD) and ground (VSS) to all parts of the chip.


## 1. Power Rings
- Placed around the core boundary.

- Connects to global VDD and VSS nets.

- Distributes power from the chip-level supply pads into the core.

- Typically implemented on metal layer M7 and M8.

## 2. Power Mesh
- Grid-like structure inside the core that distributes power uniformly.

- Interconnects macros and standard cells to the ring.

- Constructed using alternating horizontal and vertical metal layers (e.g., M6/M7).

## 3. Power Rails
- Horizontal power and ground lines within each row of standard cells.

- Connected to the power mesh using vias.

- Ensures each standard cell receives power and ground.


![Screenshot from 2025-06-19 14-56-07](https://github.com/user-attachments/assets/7a3a7332-d711-47f4-bc83-89abd2aba9e4)

 
