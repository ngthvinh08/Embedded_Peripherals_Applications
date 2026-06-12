# High-Level Applications on Embedded Peripherals

A collection of practical software architectures and application-layer implementations built on top of common microcontroller peripherals.

Instead of focusing on peripheral initialization and register configuration, this repository explores how peripherals are used in real embedded products.

---

## Motivation

Most embedded tutorials stop at:

* UART transmission and reception
* ADC sampling
* SPI communication
* I2C communication
* Timer configuration

However, real-world firmware is built on top of these peripherals.

For example:

| Peripheral | Basic Example      | High-Level Application    |
| ---------- | ------------------ | ------------------------- |
| UART       | Send a string      | AT Command Engine         |
| UART       | Receive bytes      | Packet Protocol           |
| UART       | Echo data          | CLI Shell                 |
| SPI        | Read/Write Flash   | Storage Layer             |
| I2C        | Read Sensor        | Sensor Abstraction Layer  |
| Timer      | Generate Interrupt | Task Scheduler            |
| ADC        | Read Voltage       | Battery Management System |
| DMA        | Memory Transfer    | Data Streaming Framework  |

This repository focuses on these higher-level applications.

---

# Repository Structure

```text
.
├── uart/
├── spi/
├── i2c/
├── adc/
├── timer/
├── dma/
├── rtc/
└── docs/
```

Each application contains:

```text
Application/
├── README.md
├── source/
├── diagrams/
└── examples/
```

---

# UART Applications

## AT Command Engine

A generic framework for handling AT commands.

### Features

* Command parser
* Command registration
* Response generation
* Timeout handling

### Typical Usage

```text
AT+RST
OK

AT+VERSION
Firmware v1.0.0
```

### Real Products

* Wi-Fi modules
* Cellular modules
* GNSS modules
* Bluetooth modules

---

## Packet Protocol Framework

A generic UART communication protocol.

### Features

* Packet framing
* Header parsing
* Payload extraction
* CRC verification
* Error handling

### Example Packet

```text
+-------+------+-----+------+------+
| SOF   | LEN  | CMD | DATA | CRC  |
+-------+------+-----+------+------+
```

### Real Products

* MCU-to-MCU communication
* Robotics
* Industrial control systems

---

## CLI Shell

A command-line interface running over UART.

### Features

* Runtime debugging
* Parameter configuration
* Diagnostics

### Example

```shell
> led on
OK

> wifi status
CONNECTED
```

### Real Products

* Embedded Linux devices
* Network equipment
* IoT gateways

---

## Bootloader Transport Layer

Communication layer between bootloader and host.

### Features

* Firmware update
* Data chunk transfer
* Image verification

### Real Products

* Firmware upgrade tools
* Manufacturing systems

---

# SPI Applications

## Display Framework

Graphics abstraction layer for displays.

### Features

* Drawing primitives
* Text rendering
* Bitmap rendering

### Real Products

* TFT displays
* Industrial HMIs
* Consumer electronics

---

## Flash Storage Layer

Software layer for external SPI flash.

### Features

* Sector management
* Wear leveling
* Block abstraction

### Real Products

* Data loggers
* IoT devices
* Consumer products

---

## Sensor Streaming Engine

High-speed sensor data acquisition.

### Features

* DMA integration
* Continuous streaming
* Ring buffer support

### Real Products

* IMUs
* Radar systems
* Medical devices

---

# I2C Applications

## Sensor Abstraction Layer

Provides a unified API for different sensors.

### Goal

Replace vendor-specific APIs with a common interface.

### Example

```c
sensor_read_temperature();
sensor_read_humidity();
```

### Real Products

* Sensor hubs
* Environmental monitoring systems

---

## Multi-Sensor Manager

Centralized management of multiple sensors.

### Features

* Polling scheduler
* Device discovery
* Data aggregation

---

# ADC Applications

## Battery Management System

Battery monitoring and protection.

### Features

* Voltage measurement
* Battery percentage estimation
* Low battery detection

### Real Products

* Portable devices
* IoT sensors

---

## Data Acquisition Framework

Framework for continuous sampling.

### Features

* Sampling engine
* Data buffering
* Signal processing

### Real Products

* Industrial monitoring
* Instrumentation systems

---

## Sensor Calibration Framework

Calibration utilities for analog sensors.

### Features

* Offset compensation
* Gain correction
* Linearization

---

# TIMER Applications

## Cooperative Scheduler

A lightweight task scheduler based on timer interrupts.

### Features

* Periodic tasks
* Non-blocking execution
* Deterministic timing

### Example

```c
Task_10ms();
Task_100ms();
Task_1000ms();
```

### Real Products

* Bare-metal firmware
* Low-cost embedded systems

---

## Software PWM Engine

Generate multiple PWM outputs using software.

### Features

* Multiple channels
* Adjustable duty cycle

---

## Signal Analyzer

Signal measurement utilities.

### Features

* Frequency measurement
* Duty-cycle measurement
* Pulse-width measurement

---

# DMA Applications

## UART DMA Receiver

High-performance UART reception.

### Features

* Circular buffer
* Idle line detection
* Background reception

---

## Streaming Framework

DMA-based data streaming engine.

### Features

* Double buffering
* Continuous transfer
* Low CPU utilization

### Real Products

* Audio systems
* Sensor acquisition systems

---

# RTC Applications

## Event Scheduler

Time-based event management.

### Features

* Alarm scheduling
* Timed execution

---

## Timestamp Service

Timestamp generation for logs and events.

### Real Products

* Data loggers
* Monitoring systems
* Industrial controllers

---

# Future Topics

* Modbus RTU Stack
* CAN Communication Framework
* USB CDC Framework
* USB HID Framework
* BLE GATT Framework
* MQTT Client
* OTA Update Framework
* Device Configuration Manager
* Logging Framework
* Event Framework
* State Machine Framework

---


# Hardware Platform

The primary development platform used in this repository is:

## MCU

**STM32F401RE**

Key specifications:

* ARM Cortex-M4 @ 84 MHz
* 512 KB Flash
* 96 KB SRAM
* UART / USART
* SPI
* I2C
* ADC
* DMA
* Timers
* RTC
* PWM
* Interrupt Controller (NVIC)

---

# Development Environment

All projects in this repository are developed using the STM32 ecosystem provided by STMicroelectronics.

## Required Software

### 1. STM32CubeIDE

Integrated development environment for:

* Writing C/C++ code
* Building projects
* Flashing firmware
* Debugging applications

Official Download:

https://www.st.com/en/development-tools/stm32cubeide.html

---

### 2. STM32CubeMX

Graphical configuration tool for:

* Pin configuration
* Clock tree configuration
* Peripheral initialization
* Code generation

Official Download:

https://www.st.com/en/development-tools/stm32cubemx.html

---

### 3. STM32CubeProgrammer

Programming and debugging utility.

Used for:

* Flashing firmware
* Erasing memory
* Reading device information
* Bootloader communication

Official Download:

https://www.st.com/en/development-tools/stm32cubeprog.html

---

### 4. ST-LINK Driver

Required for:

* Debugging
* Flash programming
* Serial Wire Debug (SWD)

Official Download:

https://www.st.com/en/development-tools/stsw-link009.html

---

# Installation Guide

## Install STM32CubeIDE

1. Create an ST account.
2. Download STM32CubeIDE from the official website.
3. Install using default settings.
4. Launch STM32CubeIDE.
5. Select a workspace directory.

Video Tutorial:

* STM32CubeIDE Installation and Overview

https://www.youtube.com/watch?v=wyMCPna-aP4

---

## Install STM32CubeMX

1. Download STM32CubeMX from the official website.
2. Install Java Runtime if requested.
3. Launch STM32CubeMX.
4. Log in with your ST account.
5. Download the required STM32 firmware packages.

Video Tutorial:

* STM32CubeIDE / STM32CubeMX Installation

https://www.youtube.com/watch?v=NUdFyqIAsqQ

---

# Recommended Tools

## Serial Terminal

For UART debugging:

* PuTTY
* Tera Term
* RealTerm
* MobaXterm

---

# Author
Fabian
Nguyen Thanh Vinh
K67 - UET - VNU
