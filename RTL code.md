# RTL CODE
```
module hybrid_alu ( 
input [3:0] A, B, 
input Clock, 
input [2:0] ALU_Sel, // Selects which output to drive 
output reg [3:0] Result, 
output reg C_out 
); 
wire [3:0] sum_add, sum_sub, sum_inc, sum_dec; 
wire c_add, c_sub, c_inc, c_dec; 
// Soft macro: A + B 
full_adder FA_add ( 
.A(A), 
.B(B), 
.Clock(Clock), 
.C_in(1'b0), 
.SUM(sum_add), 
.C_out(c_add) 
); 
// Soft macro: A - B = A + (~B + 1) 
full_adder FA_sub ( 
.A(A), 
.B(~B), 
.Clock(Clock), 
.C_in(1'b1), 
.SUM(sum_sub), 
.C_out(c_sub) 
); 
// Soft macro: A + 1 
full_adder FA_inc ( 
.A(A), 
.B(4'b0000), 
.Clock(Clock), 
.C_in(1'b1), 
.SUM(sum_inc), 
.C_out(c_inc) 
); 
// Soft macro: A - 1 
full_adder FA_dec ( 
.A(A), 
.B(4'b1111), // -1 in 2's comp 
.Clock(Clock), 
.C_in(1'b0), 
.SUM(sum_dec), 
.C_out(c_dec) 
); 
// Standard cell–based logic 
wire [3:0] and_op = A & B; 
wire [3:0] or_op = A | B; 
wire [3:0] xor_op = A ^ B; 
wire [3:0] not_a = ~A; 
wire [3:0] shl = A << 1; // Shift left 
wire [3:0] shr = A >> 1; // Shift right 
// Output selection 
always @ (posedge Clock) begin 
case (ALU_Sel) 
3'b000: begin Result <= sum_add; C_out <= c_add; end   // A + B 
3'b001: begin Result <= sum_sub; C_out <= c_sub; end  // A - B 
3'b010: begin Result <= sum_inc; C_out <= c_inc; end  // A + 1 
3'b011: begin Result <= sum_dec; C_out <= c_dec; end   // A - 1 
3'b100: begin Result <= and_op; C_out <= 0; end       // A AND B 
3'b101: begin Result <= or_op; C_out <= 0; end        // A OR B 
3'b110: begin Result <= xor_op; C_out <= 0; end       // A XOR B 
3'b111: begin Result <= shl; C_out <= 0; end          // Shift A left
// You can add more like NOT A or SHR if needed 
endcase 
end 
endmodule
```

##  RTL Code Explanation – `hybrid_alu.v`

This module is a **4-bit ALU** that performs different arithmetic and logic operations based on a control input called `ALU_Sel`.

###  Inputs

- `A` – 4-bit input value (first number)
- `B` – 4-bit input value (second number)
- `Clock` – Clock signal (used to update outputs on the rising edge)
- `ALU_Sel` – 3-bit control signal that chooses which operation the ALU will perform

###  Outputs

- `Result` – 4-bit output of the selected operation
- `C_out` – Carry-out bit (used in arithmetic operations)

---

###  How the ALU Works

This ALU can perform **8 different operations**, selected by the 3-bit control signal `ALU_Sel`.

| ALU_Sel | Operation | Description       |
|--------:|-----------|-------------------|
| 000     | A + B     | Add two numbers   |
| 001     | A - B     | Subtract B from A |
| 010     | A + 1     | Increment A       |
| 011     | A - 1     | Decrement A       |
| 100     | A AND B   | Bitwise AND       |
| 101     | A OR B    | Bitwise OR        |
| 110     | A XOR B   | Bitwise XOR       |
| 111     | A << 1    | Shift A left by 1 |

---

###  How Operations Are Done

####  Arithmetic Operations
These are done using a small reusable module called `full_adder`, which is connected 4 times:

- `FA_add` → A + B  
- `FA_sub` → A - B (by using A + ~B + 1)  
- `FA_inc` → A + 1  
- `FA_dec` → A - 1 (by using A + (-1))

Each `full_adder` takes A and B, adds them with a carry-in, and gives a result and a carry-out.

####  Logic Operations
These are done using simple Verilog logic operations:

- `A & B` → AND  
- `A | B` → OR  
- `A ^ B` → XOR  
- `A << 1` → Shift Left  


---

###  Output Selection

The result is selected based on `ALU_Sel` using a `case` statement inside an `always @(posedge Clock)` block. This means the output updates only on the rising edge of the clock.

---

