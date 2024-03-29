# Linuxcnc Hardware

# Hardware to run the LinuxCNC software
A computer is required to run LinuxCNC itself

The most common is to use a x86 computer (standard Intel / AMD computer)

ARM computers such as the Raspberry Pi or Orange Pi can be used

# Hardware Interface to CNC machine
There are multiple different ways to interface between LinuxCNC controller software, and CNC hardware (such as stepper / servo drivers, limits switches, inputs and outputs etc.)

Interfaces include:
- Parallel Port
- Ethernet
- Ethercat
- PCI / PCIe
- SPI (where the computer has a native SPI interface, such as Raspberry Pi)
- USB (__not realtime interface__)

A mix of different interfaces can be used. For example, a combination of ethercat for servo drives, and parallel port for additional General Purpose Inputs / Outputs (GPIO)

Some of these solutions are usable for all aspects of hardware interfacing, and some have specific roles (e.g. non-realtime GPIO, for an operator inferface).

## Parallel Port
Using onboard motherboard parallel port, or a PCI/PCIe parallel port card.

### Parallel Port Software Interface
Step generation is done in software on the LinuxCNC host - this means the parallel port interface is much more sensitive to the LinuxCNC computer's latency.

__Advantages:__
- Low cost
- Simple configuration

__Disadvantages:__
- Sensitive to the LinuxCNC computer's latency
- Limited inputs/outputs 
- Some PCI/PCIe parallel port cards do not work well or do not properly support the required EPP mode


### Parallel Port FPGA Communication
Mesa use Field-programmable gate array (FPGA) interfaced via parallel port - e.g. 7i43

Website: http://mesanet.com/    Store: http://store.mesanet.com/


## Ethernet
### Mesa Ethernet
Mesa use Field-programmable gate array (FPGA) 

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
Mesa produce Field-programmable gate array (FPGA) PCI / PCIe cards

Multiple daughter / expansion cards are available

Website: http://mesanet.com/    Store: http://store.mesanet.com/


## SPI
### Remora SPI
Realtime requirements are offloaded onto a controller board. https://remora-docs.readthedocs.io

### LinuxCNC-RIO
RealtimeIO for LinuxCNC based on an FPGA

https://github.com/multigcs/LinuxCNC-RIO

## USB
USB devices cannot be used to control motors or perform other __"real time"__ tasks.

### LinuxCNC_ArduinoConnector
This Project enables you to connect an Arduino to LinuxCNC and provides as many IO's as you could ever wish for. This Software is used as IO Expansion for LinuxCNC.
It is NOT intended for timing and security relevant IO's. Don't use it for Emergency Stops or Endstop switches!

Site: https://github.com/AlexmagToast/LinuxCNC_ArduinoConnector


