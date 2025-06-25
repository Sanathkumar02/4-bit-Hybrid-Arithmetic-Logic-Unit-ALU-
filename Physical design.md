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


# Placement

The placement view of a hierarchical 4-bit Arithmetic Logic Unit (ALU). The ALU is implemented using modular full adder blocks and includes arithmetic operations such as:

- Addition (FA_add)

- Subtraction (FA_sub)

- Increment (FA_inc)

- Decrement (FA_dec)


## Placement Strategy
The standard cell layout is divided into four quadrants, representing different arithmetic functions:

| Quadrant      | Function  | Module  |
|---------------|-----------|---------|
| Top-Left      | Increment | FA_inc  |
| Top-Right     | Decrement | FA_dec  |
| Bottom-Left   | Subtract  | FA_sub  |
| Bottom-Right  | Add       | FA_add  |



## Steps Involved in Your Placement Optimization Flow

- 1. Loading Timing Constraints
- 2. Creating Timing Scenarios
- 3. Modeling Parasitics
- 4. Initial Placement
- 5. Cell Usage Control
- 6. Activating Timing Checks
- 7. Placement Optimization
- 8. Legalization 

![Screenshot from 2025-06-19 15-14-38](https://github.com/user-attachments/assets/8d5661d9-0a04-4dc5-9bc6-a105f2bdc9fa)


# Clock Tree Synthesis (CTS)

Clock Tree Synthesis (CTS) is a crucial stage in the physical design flow where the goal is to distribute the clock signal across the entire design with minimal skew and latency, ensuring that all sequential elements receive the clock within strict timing bounds.


## 1. Design Checks Before CTS
Before beginning CTS, a design check is performed to ensure that the current design:

- Is in a legal state after placement.

- Has no structural issues that might affect CTS 

- Complies with timing and physical constraints defined in the `.sdc`.

## 2. Activating Timing Scenario
The selected scenario `func_slow` is activated to guide CTS under the worst-case process, voltage, and temperature conditions.

This includes enabling checks for:

- Setup and hold timing

- Dynamic and leakage power

- Maximum capacitance and transition

Activating the scenario ensures CTS decisions align with the overall design goals under the worst operating conditions.

## 3. Clock Tree Synthesis (CTS)
At this step:

- The clock net is identified .

- The tool inserts buffers/inverters to balance the load and minimize skew.

- The clock tree is built hierarchically to meet latency and transition targets.

- Routing resources are optimized so the clock reaches every register with minimal variation.

CTS ensures that no part of the design is starved of the clock, and timing across different ALU blocks (like FA_add, FA_sub, etc.) remains consistent.

## 4. Clock Optimization

Post-synthesis, the clock tree is optimized:

- To fine-tune skew and latency

- To reduce power consumption

- To meet post-CTS timing constraints

- Clock optimization may involve:

- Buffer resizing

- Inverter insertion/removal

- Re-routing of skewed paths

  ![Screenshot from 2025-06-19 15-18-33](https://github.com/user-attachments/assets/48709207-c847-4179-8c54-d19e2fc699f1)


 # Routing
 
Routing is a critical step in the physical design flow where all logical connections between the placed standard cells are physically realized using metal layers. This process occurs after placement and clock tree synthesis (CTS) and is responsible for ensuring that signals are properly connected while meeting all design, timing, and electrical rules.

## 1.  Global Routing
 Estimates paths between cells using a coarse grid and guides track and layer allocation while avoiding high congestion zones.

## 2. Track Assignment
 Maps each global route to a specific routing track based on layer direction and pitch. Aligns routing to fabrication-compliant tracks, preparing for detailed routing.

## 3. Detailed Routing
 Performs exact metal trace drawing, adds vias, and implements all net connections. Produces a complete and manufacturable routed layout that meets spacing and width rules.
 

## 4. Route Optimization
 
Reduce wirelength and capacitance, improve timing (especially critical paths), fix any DRCs (spacing, via, shorts).


![Screenshot from 2025-06-19 15-19-43](https://github.com/user-attachments/assets/02ac3f32-68c9-4b30-98db-d55dbe7cbd5f)

 

