## Synchronous TX–RX Serial Communication System

## Overview
This project implements a complete **synchronous serial communication system** in **SystemVerilog**.  
The design includes a **Transmitter (TX)**, **Receiver (RX)**, **ROM and RAM memory blocks**, and **FSM-based control logic** to serialize, transmit, deserialize, and store data reliably.

The system models the **core architecture of a USART**, but without asynchronous baud-rate generation, start/stop bit framing, or parity logic. All transfers are synchronized to a common clock.

---

## Architecture
The design is composed of the following major blocks:

### TX Block
- FSM-controlled serializer  
- ROM-based data source  
- Shift register outputs serial data (LSB first)  
- Handshake signaling (`tx_valid`, `rx_ready`)  
- Completion signaling (`tx_finish`)

### RX Block
- FSM-controlled deserializer  
- Shift register collects serial bits  
- RAM-based data storage  
- Address counter for memory writes  
- Completion signaling (`rx_finish`)

### Control Strategy
- Moore-style FSMs  
- Clean separation of control and datapath  
- Deterministic, cycle-accurate behavior  

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
│   └── rx_ram.sv    # RX RAM (data storage)
├── sim/
│   └── tx_rx_tb.sv  # Testbench
├── memory/
│   └── memory.list  # ROM initialization file
├── docs/
│   └── waveforms.png # Simulation waveform screenshots
└── README.md

