# i2c-remapper-fpga
# I2C Address Translator Project

## Project Overview  
This repository contains the design and verification of an I²C address-translator implemented in FPGA logic. A master device communicates with two slaves having the same default address (`0x48`); the translator intercepts and remaps one of them transparently so the master can access both without conflict.

## Key Features  
- Two I²C slaves with identical default address `0x48`.  
- Translator module maps one slave to a **virtual address** (for example `0x49`) so that both slaves can coexist on the same bus.  
- Master device sees both slaves as separate addresses, while the translator handles the remapping internally.  
- Full testbench and simulation available via **EDA Playground**: [Link](https://edaplayground.com/x/LZBi)

## Design Structure  
- `design.sv` (or `.v`): Contains the translator logic module, slaved-interface logic, and address-remapping logic.  
- `testbench.sv`: Stimulus for I²C transactions (read/write) to both slave addresses, verifying correct behavior.  
- Simulation target: I²C master issues requests, translator monitors address, when it sees `0x48` for Slave 2 it converts to virtual address `0x49`, forwards to Slave 2; when it sees `0x48` for Slave 1 it forwards unchanged.  
- Bus timing, acks, and data transfer properly handled per I²C specification.

## How to Run / Simulation Instructions  
1. Open the link on EDA Playground: [https://edaplayground.com/x/LZBi](https://edaplayground.com/x/LZBi)  
2. Select appropriate simulator (e.g., Icarus Verilog / Synopsys VCS).  
3. Run the simulation.  
4. Observe log output:  
   - Access to Slave 1 at address `0x48` should succeed with expected data.  
   - Access to Slave 2 (via virtual address `0x49`) should also succeed, showing remapping functionality.  
5. Review waveforms (if available) or log traces to verify address translation and data transaction.

## Repository Structure
