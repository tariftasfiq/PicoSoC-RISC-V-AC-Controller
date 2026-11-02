# PicoSoC-Based RISC-V AC Controller

**A RISC-V-based System-on-Chip (SoC) implementation for an AC controller application.**

This project focuses on the design and implementation of an application-specific System-on-Chip based on the PicoSoC architecture and the 32-bit RISC-V processor. The repository contains the hardware description, design configurations, timing constraints, and supporting scripts used throughout the development and implementation process.

The project explores the integration of a programmable processor-based system with application-specific control functionality, targeting an ASIC implementation using an open-source digital design flow.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Design Objectives](#design-objectives)
- [System Architecture](#system-architecture)
- [Hardware Architecture](#hardware-architecture)
- [RTL Design and Integration](#rtl-design-and-integration)
- [ASIC Implementation Flow](#asic-implementation-flow)
- [Timing Constraints](#timing-constraints)
- [Physical Design Configuration](#physical-design-configuration)
- [Repository Structure](#repository-structure)
- [Technology and Tools](#technology-and-tools)
- [Getting Started](#getting-started)
- [Implementation and Verification](#implementation-and-verification)
- [Future Improvements](#future-improvements)
- [Acknowledgements](#acknowledgements)
- [Author](#author)

---

## Project Overview

The objective of this project is to implement a RISC-V-based SoC for an AC controller application using the PicoSoC platform.

PicoSoC provides a compact processor-based architecture that can be extended with application-specific hardware and software functionality. Building on this architecture, the project involves adapting and integrating the processor subsystem, configuring the hardware design, and preparing the implementation for ASIC physical design.

The project covers important stages of digital IC development, including:

- Understanding and adapting an existing RISC-V SoC architecture.
- RTL integration and hardware configuration.
- Processor and peripheral subsystem integration.
- Timing constraint definition.
- Logic synthesis.
- Floorplanning and physical implementation.
- Physical verification and implementation assessment.

The repository serves as the working design environment for the PicoSoC-based AC controller implementation.

## Design Objectives

The major objectives are:

1. Develop a processor-based SoC architecture for an AC controller application.
2. Utilize the PicoSoC architecture and its RISC-V processing subsystem.
3. Organize and configure the RTL source files for the target implementation.
4. Establish the timing and physical-design constraints.
5. Prepare the design for synthesis and ASIC implementation.
6. Evaluate the design through functional and physical verification workflows.

## System Architecture

The system is based on the PicoSoC architecture, which integrates a RISC-V processor with memory and peripheral interfaces.

At a conceptual level, the system can be represented as:

```text
             +--------------------------+
             |       PicoSoC System     |
             |                          |
             |    +----------------+    |
             |    |  RISC-V CPU    |    |
             |    +-------+--------+    |
             |            |             |
             |     System Interconnect  |
             |            |             |
             |    +-------+--------+    |
             |    |                |    |
             |  Memory          Peripherals
             |    |                |    |
             |  +------+      +----+---+|
             |  | SRAM |      | SPI    ||
             |  +------+      | UART   ||
             |                +--------+|
             +------------+-------------+
                          |
                          |
                 AC Controller Logic
                          |
                 Application Interface
```

*Note: This is a conceptual architecture diagram. Refer to the actual RTL hierarchy for the implemented module connections and application-specific interfaces.*

## Hardware Architecture

### RISC-V Processing Subsystem

The processing subsystem is based on the PicoSoC architecture, which uses the PicoRV32 RISC-V processor core.

The processor provides the programmable execution environment for application-level control and communication with the integrated hardware components.

### Memory Subsystem

The memory subsystem provides storage for processor instructions, data, and runtime operations.

The exact memory organization and implementation depend on the selected configuration and memory integration used in the design.

### Peripheral Interfaces

The PicoSoC architecture provides peripheral interfaces that support communication between the processor and external or application-specific hardware.

The project configuration and RTL should be consulted for the exact peripherals and interfaces enabled in the final implementation.

### AC Controller Application

The application-specific objective is to use the processor-based SoC as the computational and control platform for an AC controller.

The control functionality is intended to be organized around the processor subsystem and its hardware interfaces. The actual control algorithms, peripheral connections, and external interfaces should be documented according to the corresponding RTL and firmware implementation.

---

## RTL Design and Integration

The RTL design is organized around the PicoSoC architecture and its supporting hardware modules.

The integration process involves:

- Identifying the top-level design and its dependencies.
- Configuring the processor and supporting modules.
- Integrating the required memory and peripheral interfaces.
- Establishing the top-level signal connections.
- Preparing the RTL source list for synthesis.

The Verilog source files under the `src/` directory contain the hardware description used by the implementation flow.

## ASIC Implementation Flow

The project follows an RTL-to-GDSII-oriented digital implementation methodology.

The major stages are described below.

### 1. RTL Preparation

The required Verilog source files are organized and configured for the target design.

The top-level module, source dependencies, technology settings, and implementation parameters are specified through the project configuration.

### 2. Logic Synthesis

Logic synthesis converts the RTL description into a technology-mapped gate-level netlist.

Yosys can be used to perform synthesis, optimize the logic, and map the design to the target standard-cell library.

Typical synthesis activities include:

- RTL elaboration.
- Hierarchy analysis.
- Logic optimization.
- Technology mapping.
- Netlist generation.

### 3. Floorplanning

Floorplanning establishes the physical dimensions and organization of the design.

Important parameters include:

- Die area.
- Core area.
- Placement utilization.
- Standard-cell placement region.
- Power and ground planning requirements.
- Macro placement, where applicable.

### 4. Placement

The placement stage assigns physical locations to the standard cells while considering timing, congestion, and design constraints.

### 5. Clock Tree Synthesis

Clock tree synthesis establishes the clock distribution network for sequential elements.

The implementation must account for clock latency, skew, and transition requirements.

### 6. Routing

The routing stage creates the physical interconnections between the placed standard cells.

Routing must satisfy the applicable technology design rules while considering signal integrity and timing requirements.

### 7. Physical Verification

The resulting physical layout is evaluated against the applicable physical design rules.

KLayout can be used for layout inspection and design-rule checking when configured with the appropriate technology rules.

### 8. GDSII Generation

The final layout data can be exported in GDSII format for downstream physical verification and fabrication preparation.

*The exact completion status of individual implementation stages should be reported using the actual run logs and sign-off results.*

---

## Timing Constraints

The timing constraints are defined in the SDC file:

`constraint.sdc`

Timing constraints communicate the operating requirements of the design to synthesis and physical implementation tools.

Typical constraint categories include:

- Clock definition.
- Clock period.
- Input delay.
- Output delay.
- Input transition.
- Output load.
- Timing exceptions, where applicable.

The actual timing values should be taken directly from the committed SDC file.

## Physical Design Configuration

The repository includes configuration files and scripts that support the implementation flow.

These files define the design parameters, source dependencies, technology configuration, timing requirements, and physical-design settings.

The configuration should be reviewed before executing the implementation flow, particularly when changing the local PDK installation or technology-library paths.

---

## Repository Structure

The repository contains the RTL source files and supporting configuration files for the project.

```text
PicoSoC-RISC-V-AC-Controller/
│
├── src/
│   └── RTL source files
│
├── config.mk
├── config_mother.mk
├── constraint.sdc
├── less_pad.tcl
├── pad.tcl
├── macro.cfg
├── rules-base.json
│
└── README.md
```

*This is a high-level representation. The actual repository tree should be used as the authoritative directory structure.*

### Configuration Files

| File | Purpose |
|---|---|
| `config.mk` | Main design and implementation configuration |
| `config_mother.mk` | Alternative configuration |
| `constraint.sdc` | Static timing constraints |
| `less_pad.tcl` | Pad placement configuration |
| `pad.tcl` | Pad placement script |
| `macro.cfg` | Macro placement configuration |
| `rules-base.json` | Supporting implementation rules |
| `src/` | RTL source files |

---

## Technology and Tools

The project uses or is organized around the following technologies and tools:

| Category | Technology / Tool |
|---|---|
| Processor architecture | RISC-V |
| SoC platform | PicoSoC |
| Hardware description | Verilog HDL |
| Logic synthesis | Yosys |
| Physical implementation | OpenROAD |
| Layout inspection and verification | KLayout |
| Timing constraints | SDC |
| Physical layout format | GDSII |
| Target technology | Refer to the committed technology configuration |

---

## Getting Started

### Prerequisites

Before attempting to run the design flow, prepare:

1. A compatible Linux environment.
2. The required RTL source files and dependencies.
3. The relevant synthesis and physical-design tools.
4. The target technology PDK and standard-cell libraries.
5. The required technology LEF, cell LEF, and GDS files, where applicable.
6. The correct environment variables and technology configuration.

### Clone the Repository

```bash
git clone https://github.com/tariftasfiq/PicoSoC-RISC-V-AC-Controller.git

cd PicoSoC-RISC-V-AC-Controller
```

### Review the Configuration

Before running the flow, review:

- `config.mk`
- `config_mother.mk`
- `constraint.sdc`
- The Tcl scripts
- The technology and library paths

Update environment-specific paths to match your local installation.

### Running the Implementation Flow

The exact commands depend on the implementation-flow scripts and tool setup included in the project.

Consult the configuration files and the corresponding flow documentation before executing synthesis or physical-design stages.

---

## Implementation and Verification

The design should be evaluated at multiple levels.

### Functional Verification

Functional verification evaluates whether the RTL implements the intended behavior.

Relevant verification activities include:

- Processor subsystem functionality.
- Memory and peripheral interfaces.
- Application-specific control behavior.
- Reset and clock behavior.
- Top-level system integration.

### Synthesis Evaluation

Synthesis reports can be used to evaluate:

- Total cell count.
- Sequential and combinational cell distribution.
- Logic utilization.
- Technology mapping.
- Area estimates.

### Physical Design Evaluation

Physical implementation reports can be used to assess:

- Core and die area.
- Placement utilization.
- Routing completion.
- Signal-metal area.
- Timing performance.
- Design-rule violations.

### Sign-off and Final Outputs

The final implementation should be evaluated using the applicable physical verification and timing sign-off reports.

Do not interpret successful GDSII generation alone as proof of complete physical sign-off.

---

## Future Improvements

Potential areas for further development include:

- More detailed documentation of the AC controller architecture.
- Expanded RTL-level verification and testbench coverage.
- Processor-to-peripheral interface documentation.
- Synthesis and physical-design report analysis.
- Power, performance, and area optimization.
- Post-silicon testing and characterization, where applicable.

---

## Acknowledgements

The project builds on the PicoSoC architecture and the open-source RISC-V and EDA ecosystem.

Thanks to the developers and maintainers of the open-source tools and technology resources that support accessible digital IC design and implementation.

## Author

**Sheikh Tariful Islam**

GitHub: [@tariftasfiq](https://github.com/tariftasfiq)

---

*This repository is maintained as part of ongoing work in RISC-V-based SoC design and digital IC implementation.*
