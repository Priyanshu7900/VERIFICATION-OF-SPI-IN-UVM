# **Verification of SPI Memory in UVM**

## **Project Overview**

This project implements the **SPI Memory Verification Environment** using **SystemVerilog** and **UVM (Universal Verification Methodology)**.  
The DUT is an SPI‑based memory module supporting read and write operations via SPI protocol.  
Verification is performed using a reusable, layered UVM testbench following industry-standard practices, aimed at ensuring reliability and maintainability.

The testbench covers both **write** and **read** transactions, ensures **protocol compliance**, and enables **functional coverage** for thorough validation.

---

## **Features**

- **UVM‑based layered testbench** designed for modularity and reuse  
- Supports both **write (W)** and **read (R)** SPI paths  
- Supports both **constrained‑random** and **directed** stimulus generation  
- **Scoreboard** for automatic result checking  
- **Coverage‑driven verification** for completeness  
- **Protocol compliance checks** for SPI signals (CS, SCLK, MOSI, MISO, data transfer correctness)  
- Simulation logs and waveforms to demonstrate correct behavior  

---

## **Architecture**

The project consists of the following key files and components:

- **spi_memory.sv** – Implements the SPI Memory DUT, handling SPI protocol signals (CS, SCLK, MOSI, MISO) and internal memory storage for read/write operations.  
- **spi_memory_tb.sv** – Testbench that instantiates the DUT, UVM environment, and starts the simulation.  
- **Interface, UVM components, and environment files** – Structured following standard UVM layering (sequencer, sequence, driver, monitor, scoreboard, environment, test files). These may include:
  - `transaction.sv` – Defines SPI memory read/write transaction items (address, data, and operation type).
  - `sequence.sv` – Generates randomized or directed sequences of read/write transactions.
  - `sequencer.sv` – Sends generated transactions to the driver.
  - `driver.sv` – Drives the SPI interface signals to interact with the DUT based on sequence instructions.
  - `monitor.sv` – Observes SPI communication from the DUT and collects transaction results.
  - `scoreboard.sv` – Compares expected vs. actual results to determine pass/fail.
  - `env.sv` – UVM environment that instantiates and wires the sequencer, driver, monitor, and scoreboard.
  - `test.sv` – UVM test definitions that configure and run various verification scenarios.
- **verification_results/** – Directory containing simulation logs, waveform files (e.g., VCD/FSDB), and coverage reports demonstrating verification outcomes.

---

## **Run on EDA Playground**

1. Visit [EDA Playground](https://www.edaplayground.com/)  
2. Set **Language** to *SystemVerilog*  
3. Add the following files:
   - `spi_memory.sv`
   - `spi_memory_tb.sv`
   - All UVM-related testbench files (e.g., sequences, driver, monitor, scoreboard, environment, test)
4. In the Testbench pane, include:
```verilog
`include "uvm_macros.svh"
`include "spi_memory.sv"
`include "spi_memory_tb.sv"
// Include all other UVM TB files here
```
5. Select a simulator that supports UVM (e.g., **Siemens Questa** or **Aldec Riviera**)  
6. Enable waveform output (e.g., Open EPWave)  
7. **Click Run** to execute the simulation  

---

## **Verification Methodology**

- **UVM‑based testbench** structured for reusability and scalability  
- Supports **directed** and **constrained‑random** transaction generation  
- **Functional coverage** ensures design requirements and corner cases are exercised  
- **Scoreboard** automatically verifies the DUT’s behavior  
- **Waveform logs** facilitate debugging and validation  

---

## **Repository Structure**

```
VERIFICATION-OF-SPI_MEMORY-IN-UVM/
│
├── src/                    # DUT and interface files
│   ├── spi_memory.sv       # SPI Memory DUT
│   └── (optional) interface.sv
│
├── tb/                     # UVM testbench files
│   ├── transaction.sv
│   ├── sequence.sv
│   ├── sequencer.sv
│   ├── driver.sv
│   ├── monitor.sv
│   ├── scoreboard.sv
│   ├── env.sv
│   └── test.sv
│
├── verification_results/   # Simulation logs, waveforms, coverage reports
├── spi_memory_tb.sv        # Top-level testbench
└── README.md
```
