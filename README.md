# Synchronous TX–RX Serial Communication System  
**SystemVerilog | RTL Design | FSM-Controlled Datapath**

---

## Overview

This project implements a **complete synchronous serial communication system** in **SystemVerilog**, designed to demonstrate **end-to-end RTL system architecture**.

The system includes a **Transmitter (TX)** and **Receiver (RX)** pair, controlled by **Moore-style finite state machines**, and integrates **ROM-based data sourcing** with **RAM-based data storage**. Data is serialized, transmitted, deserialized, and written to memory using **cycle-accurate, handshake-driven control logic**.

This design models the **core architecture of a USART-style system**, intentionally excluding asynchronous baud-rate generation and framing in order to focus on **clean RTL structure, FSM/datapath separation, and verification-driven design**.

---

## Project Motivation

The goal of this project was to demonstrate practical **digital design skills** relevant to FPGA and ASIC development, including:

- FSM-controlled datapaths  
- Serial data transfer using shift registers  
- Memory modeling in RTL  
- Handshake-based flow control  
- Debugging and verification using waveform analysis  

This project reflects **industry-style RTL design practices**, rather than a minimal academic example.

---

## System Architecture

The design is composed of the following major blocks:

### Transmitter (TX) Block
- FSM-controlled serializer  
- ROM-based data source  
- Shift-register-based serialization (LSB first)  
- Handshake signaling (`tx_valid`, `rx_ready`)  
- Completion signaling (`tx_finish`)  

### Receiver (RX) Block
- FSM-controlled deserializer  
- Shift register for serial bit collection  
- RAM-based data storage  
- Address counter for memory writes  
- Completion signaling (`rx_finish`)  

### Control Strategy
- Moore-style FSMs  
- Clean separation between **control logic** and **datapath**  
- Deterministic, cycle-accurate behavior  
- Synchronous operation using a shared clock domain  

---

## File Structure

```text
tx_rx_project/
├── src/
│   ├── tx.sv        # TX top module
│   ├── tx_sm.sv     # TX FSM
│   ├── tx_rom.sv    # TX ROM (read-only data source)
│   ├── rx.sv        # RX top module
│   ├── rx_sm.sv     # RX FSM
│   ├── rx_ram.sv    # RX RAM (data storage)
│
├── sim/
│   └── tx_rx_tb.sv  # Self-checking testbench
│
├── memory/
│   └── memory.list  # ROM initialization file
│
├── docs/
│   └── waveforms.png # Simulation waveform screenshots
│
└── README.md
```
---

## Simulation
- Simulated using **Vivado Simulator (xsim)**
- Verified correct operation for:
  - FSM sequencing
  - Bit-level shifting
  - ROM reads and RAM writes
  - Handshake flow control
  - Completion signaling (`tx_finish`, `rx_finish`)

### Simulation Waveforms
Representative waveforms are provided in `docs/waveforms.png`,
showing TX serialization, RX deserialization, memory writes,
and completion signaling. 
---

## Key Learning Outcomes
- FSM and datapath separation
- Shift-register-based serial communication
- Memory modeling in RTL
- Handshake-based control signaling
- Cycle-accurate simulation and debugging
- Hierarchical RTL design practices

---

## Relation to USART
This project is **conceptually similar to a USART**, but operates synchronously:
- No baud-rate generator
- No start/stop bits
- No parity logic

It focuses on the **core TX/RX architecture**, making it an ideal foundation for extending toward a full UART/USART implementation.

---

## Future Improvements
- Baud-rate generator
- Start/stop bit framing
- Parity checking
- Error detection and recovery
- Asynchronous clock domain support

---

## Tools Used
- Vivado ML Editions
- **Language:** SystemVerilog
- **Simulator:** Vivado Simulator (xsim)
- **Version Control:** Git / GitHub

---

---

## Author
**Derrick Smith**  
Embedded Systems Development & Digital Design  
FPGA • RTL • SystemVerilog • Verification

