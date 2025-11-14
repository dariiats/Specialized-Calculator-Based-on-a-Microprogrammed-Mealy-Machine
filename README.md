# Specialized-Calculator-Based-on-a-Microprogrammed-Mealy-Machine
This repository contains the implementation of a specialized arithmetic calculator built on top of a microprogrammed Mealy-type control unit.

The device processes an array of 8-bit signed (two’s complement) values according to a predefined algorithm and communicates through an 8-bit bidirectional data bus with TTL-compatible control signals.
The control logic is implemented using a ROM-based microprogram and a state register, forming a microprogrammed control unit (MPA).
<img width="1003" height="1446" alt="image" src="https://github.com/user-attachments/assets/ba68c3d0-e5e1-4d0b-a483-d673586b6df8" />

## Main Elements of the Circuit
- IDT6116SA – 2K×8 Static RAM

- AT28C64B – 8-KB EEPROM (used as ROM)

- DM74LS193 – 4-bit Up/Down Counter

- SN74S283 / SN74LS283 – 4-bit Binary Adders

- 74374 – 8-bit D-type Register with Tri-State Outputs

- 74198 / 74F198 – 8-bit Bidirectional Shift Register

- DM74ALS245A – 8-bit Bidirectional Bus Transceiver

- 7408 – Quad 2-Input AND Gate

- 4073 – Triple 3-Input AND Gate

- 7432 – Quad 2-Input OR Gate

- 4075 – Triple 3-Input OR Gate

- SN7404N – Hex Inverter

- Clock generator

- Reset circuitry

- 8-bit bidirectional data bus (TTL-compatible)
## Project Components
The repository includes several core binary modules that represent the memory contents used by the calculator. These files contain pre-generated data sets, microprogram instructions, and auxiliary control information required for correct operation of the system.
### Binary Files (.bin)
.bin files represent the contents of ROM and RAM blocks used in the system simulation.
These files allow:

- loading predefined values into memory during simulation,

- initializing control logic of the microprogrammed unit,

- ensuring that the calculator follows a deterministic execution sequence.

All binaries are ready to be imported directly into Proteus memory components.

### Microcode Table 
Alongside the binary files, the repository includes the complete microprogram table (also referred to as the firmware table).
This table defines:

- state transitions of the microprogrammed control unit,

- output control signals for each microcommand,

- addressing rules for ROM entries.

The firmware table serves both as documentation of the control logic and as the source used to generate the .bin ROM files.
It allows anyone to understand, modify, or regenerate the microprogram if needed.

## Algorithm Description
For each element X[i], the calculator computes: RESULT = (-7 * X[i] + 3 * X[i+1])/8

1. Wait for START

The system remains idle until the START signal is received.

2. Load input data into memory

Incoming values are written sequentially into RAM.

Main processing loop (for each element X[i]):

- Read X[i]

- Add X[i] to itself seven times

- Convert the obtained sum to a negative value

- Read X[i+1]

- Add X[i+1] to the result three times
 
- Shift the result three times to the right 

- Store the final value back into memory at position X[i]

3. Final output phase
   
After processing all elements, the system reads resulting values from memory and outputs them one by one.

