# Linuxcnc Hardware

# Hardware to run the LinuxCNC software
A computer is required to run LinuxCNC itself.

Minimum computer requirements can be found in the LinuxCNC docs: http://linuxcnc.org/docs/stable/html/getting-started/system-requirements.html

The most common is to use a x86 computer (standard Intel / AMD computer)

ARM computers such as the Raspberry Pi or Orange Pi can be used

# Hardware Interface to CNC machine
There are multiple different ways to interface between LinuxCNC controller software, and CNC hardware (such as stepper / servo drivers, limit switches, inputs and outputs etc.)

Interfaces include:
- Parallel Port
- Ethernet
- Ethercat
- PCI / PCIe
- SPI (where the computer has a native SPI interface, such as Raspberry Pi)
- USB (__not__ realtime interface)

A mix of different interfaces can be used. For example, a combination of ethercat for servo drives, and parallel port for additional General Purpose Inputs / Outputs (GPIO)

Some of these solutions are usable for all aspects of hardware interfacing, and some have specific roles (e.g. non-realtime GPIO, for an operator inferface).

## Parallel Port
Using onboard motherboard parallel port, or a PCI/PCIe parallel port card.

## Parallel Port Software Interface
Realtime (time critical) tasks such as step generation are done in software on the LinuxCNC host - this means the parallel port interface is much more sensitive to the LinuxCNC computer's latency.

__Advantages:__
- Low cost
- Simple configuration

__Disadvantages:__
- Sensitive to the LinuxCNC computer's latency
- Limited inputs/outputs 
- Some PCI/PCIe parallel port cards do not work well or do not properly support the required EPP mode


## Parallel Port FPGA Communication
Realtime (time critical) tasks such as step generation are done in hardware (not on the computer)

### Mesa via Parallel Port
Mesa use Field-programmable gate array (FPGA) interfaced via parallel port - e.g. 7i43

Website: http://mesanet.com/    Store: http://store.mesanet.com/

### Pico Systems via Parallel Port
http://pico-systems.com/univstep.html


## Ethernet
### Mesa Ethernet
Mesa cards with a Field-programmable gate array (FPGA), interfaced to LinuxCNC computer via Ethernet. Time critical (realtime) tasks are performed on the FPGA card.

Multiple ethernet interface FPGA cards are available, with many expansion cards

Website: http://mesanet.com/    Store: http://store.mesanet.com/

### Remora Ethernet
Realtime requirements are offloaded onto a controller board. Multiple differnet controller boards are supported - see Remora docs

Remora docs: https://remora-docs.readthedocs.io

As of March 2024:
```
STM32 based controller boards

    NVEM - an STM32F207 based board with Ethernet PHY chip, originally intended for Mach3. [No longer in production, Legacy Support - no new features]

    EC500 - an STM32F407 based board with Ethernet PHY chip, originally intended for Mach3. [No longer in production, Legacy Support - no new features]

    Expatria Technologies Flexi-HAL with uFlexiNET Ethernet adapter - an STM32F446 based board with W5500 Ethernet SPI adapter designed for Remora

iMX RT1052 based controller boards

    NVEM, EC300 & EC500 - iMXRT1052 based controller boards with Ethernet PHY chip, originally intended for Mach3. [In active development]

RP2040 based controller boards

    WIZnet W5500-EVB-Pico - Raspberry Pi RP2040 based development board with on-board W5500 Ethernet SPI adapter

    Expatria Technologies PicoBOB-DLX - Raspberry Pi RP2040 based board with on-board W5500 Ethernet SPI adapter designed for Remora
```

### Litex-CNC
This project aims to make a generic CNC firmware and driver for FPGA cards which are supported by LiteX. Configuration of the board and driver is done using json-files. The supported boards are the Colorlight boards 5A-75B and 5A-75E, as these are fully supported with the open source toolchain.

Colorlight 5A-75B and 5A-75E cards are designed as a LED receiver card - it outputs to LED matrix panels. These cards have outputs only - hardware modification is required to enable use for inputs. Soldering required. Output buffers can be replaced with an input buffer.

https://litex-cnc.readthedocs.io


### LinuxCNC-RIO
RealtimeIO for LinuxCNC based on an FPGA

Ethernet interface can be used with a Ethernet to SPI interface.

https://github.com/multigcs/LinuxCNC-RIO


## Ethercat
Beckhoff EtherCAT(TM) and compatible systems can be made to work with LinuxCNC using the open source etherlab software.

EtherCAT is the open real-time Ethernet network originally developed by Beckhoff.
The EtherCat master (LinuxCNC computer) uses a standard ethernet (network) interface - no special hardware is needed on the master. The slaves use special hardware.
There are many EtherCat slave devices available including servo drives, stepper drives, input, output interfaces, VFDs, and others.


## PCI / PCIe
### Mesa
Mesa PCI / PCIe cards with a Field-programmable gate array (FPGA). Time critical (realtime) tasks are performed on the FPGA card.

Multiple daughter / expansion cards are available

Website: http://mesanet.com/    Store: http://store.mesanet.com/

## SPI
SPI = Serial Peripheral Interface. SPI interfaces can be found on single board computers like Raspberry Pi, or Orange Pi. SPI interface is __not__ generally present on standard computers (AMD/Intel).


### Remora SPI
Realtime requirements are offloaded onto a controller board. https://remora-docs.readthedocs.io

### LinuxCNC-RIO
RealtimeIO for LinuxCNC based on an FPGA

https://github.com/multigcs/LinuxCNC-RIO

### Mesa
Mesa cards with a Field-programmable gate array (FPGA), interfaced to LinuxCNC computer via SPI. Time critical (realtime) tasks are performed on the FPGA card.

Example: 7C80 for Raspberry Pi

Website: http://mesanet.com/    Store: http://store.mesanet.com/


## USB
USB devices cannot be used to control motors or perform other __"real time"__ tasks.

### LinuxCNC_ArduinoConnector
This Project enables you to connect an Arduino to LinuxCNC and provides as many IO's as you could ever wish for. This Software is used as IO Expansion for LinuxCNC.
It is NOT intended for timing and security relevant IO's. Don't use it for Emergency Stops or Endstop switches!

Site: https://github.com/AlexmagToast/LinuxCNC_ArduinoConnector


