# 4:1 Multiplexer Implementation in Spartan-7 FPGA

## Aim
To design, synthesize, and implement a 4:1 Multiplexer using Verilog HDL on a Spartan-7 FPGA using Xilinx Vivado Design Suite.



## Apparatus Required
| S.No | Apparatus / Software | Specification / Description |
|------|----------------------|-----------------------------|
| 1 | FPGA Board | Xilinx Spartan-7 development board  |
| 2 | Software | Xilinx Vivado Design Suite  |
| 3 | Cable | USB Programming Cable (JTAG/USB-JTAG) |



## Theory
A **4:1 multiplexer** selects one of four data inputs (i0..i3) and routes it to a single output y, based on two select lines sel[1:0].

**Truth table**

| S1 | S0 | Y   |
|----|----|-----|
| 0  | 0  | D0  |
| 0  | 1  | D1  |
| 1  | 0  | D2  |
| 1  | 1  | D3  |

**Logic Diagram:**
<img width="463" height="368" alt="image" src="https://github.com/user-attachments/assets/7e2b9a82-5482-4265-8007-4c3761706314" />



## Procedure (Vivado Design Suite)

1. **Create Project**
   - Open Vivado → *Create New Project*.
   - Name project `MUX_4to1_Spartan7`. Select *RTL Project*, enable *Do not specify sources at this time* (or add immediately).
   - Choose the correct Spartan-7 device/board for your hardware.

2. **Create Design Source**
   - Flow Navigator → *Add Sources* → *Add or Create Design Sources*.
   - Create file `mux4to1.v` and type the Verilog code.

3.  **Add Constraints**
   - Add XDC file `mux4to1.xdc` and map inputs/outputs to board pins.

4.  **Synthesize & Implement**
   - Run *Synthesis* → inspect warnings/errors.
   - Run *Implementation* → review timing and utilization.

5. **Generate Bitstream & Program**
   - Generate Bitstream.
   - Open *Hardware Manager* → connect to target → Program device with `.bit` file.
   - Verify outputs on LEDs/scope.

## Verilog Program (`mux4to1.v`)

```
module mux(
    input [3:0] i,
    input [1:0] s,
    output y
    );

wire [4:1]w;
assign w[1]=i[0]&(~s[1])&(~s[0]);
assign w[2]=i[1]&(~s[1])&s[0];
assign w[3]=i[2]&s[1]&(~s[0]);
assign w[4]=i[3]&s[1]&s[0];
assign y=w[1]|w[2]|w[3]|w[4];
endmodule


```
## Constraint file for Seven-Segment Display
```
set_property -dict {PACKAGE_PIN V2 IOSTANDARD LVCMOS33} [get_ports {i[0]}]
set_property -dict {PACKAGE_PIN U2 IOSTANDARD LVCMOS33} [get_ports {i[1]}]
set_property -dict {PACKAGE_PIN U1 IOSTANDARD LVCMOS33} [get_ports {i[2]}]
set_property -dict {PACKAGE_PIN T2 IOSTANDARD LVCMOS33} [get_ports {i[3]}]
set_property -dict {PACKAGE_PIN K2 IOSTANDARD LVCMOS33} [get_ports {s[0]}]
set_property -dict {PACKAGE_PIN K1 IOSTANDARD LVCMOS33} [get_ports {s[1]}]

set_property -dict {PACKAGE_PIN G1 IOSTANDARD LVCMOS33} [get_ports {y}]

```
## FPGA Implementation Output

<img width="993" height="688" alt="image" src="https://github.com/user-attachments/assets/ed33f844-0a85-4e31-b5e3-93269c74769c" />


## Conclusion

The 4:1 multiplexer was successfully designed,synthesized, and implemented (bitstream generated) in the Spartan-7 FPGA. The output matches the expected truth table.
# 4-to-1-MUX-Implementation-in-Spartan-7-FPGA
