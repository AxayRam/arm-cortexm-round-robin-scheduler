# ARM Cortex-M Round Robin Task Scheduler

## Overview

This project implements a simple Round Robin Task Scheduler on an ARM Cortex-M microcontroller using bare-metal ARMv7-M Assembly.

The scheduler demonstrates how multitasking can be achieved without an RTOS by manually performing context switching between tasks using separate stacks and SysTick timer interrupts.

The project was developed to understand the internal working principles of embedded operating systems and real-time schedulers.

---

## Features

* Round Robin Scheduling
* Three Independent Tasks
* Dedicated Stack for Each Task
* Manual Context Switching
* SysTick Interrupt Based Scheduling
* ARM Cortex-M Assembly Implementation
* QEMU Based Simulation
* GDB Debugging Support

---

## System Architecture

The scheduler maintains:

* Task 1 Stack
* Task 2 Stack
* Task 3 Stack

Each task owns its own stack memory region.

When a SysTick interrupt occurs:

1. Current task context is saved.
2. Scheduler selects the next task.
3. Next task context is restored.
4. Execution resumes from the next task.

This process creates cooperative multitasking behavior on a single-core processor.

---

## Context Switching Process

### Save Context

The scheduler saves:

* R4-R11 Registers
* Current Stack Pointer

### Select Next Task

Round Robin Sequence:

Task1 → Task2 → Task3 → Task1

### Restore Context

The scheduler restores:

* Saved Stack Pointer
* Saved Registers

Execution then continues from the previously interrupted instruction.

---

## Tools Used

### Development

* ARMv7-M Assembly
* GNU Arm Toolchain

### Debugging

* GDB
* QEMU

### Concepts

* Context Switching
* Interrupt Handling
* Stack Management
* Embedded Scheduling
* Bare-Metal Firmware Development

---

## Build

```bash
make
```

## Run

```bash
qemu-system-arm -M lm3s6965evb -kernel scheduler.elf
```

## Debug

Terminal 1:

```bash
qemu-system-arm -M lm3s6965evb -kernel scheduler.elf -S -gdb tcp::1234
```

Terminal 2:

```bash
gdb-multiarch scheduler.elf
```

Inside GDB:

```gdb
target remote localhost:1234
layout asm
info registers
```

---

## Learning Outcomes

Through this project I gained practical understanding of:

* CPU Register Preservation
* Stack Pointer Manipulation
* Interrupt Driven Scheduling
* Task Isolation
* ARM Cortex-M Exception Handling
* RTOS Internals
* Low-Level Firmware Development

---

## Future Improvements

* Priority-Based Scheduling
* Dynamic Task Creation
* PendSV Context Switching
* Tickless Scheduling
* Mutex and Semaphore Support
* C Language Port

---

## Author

Jayraj Baldaniya

Electronics and Communication Engineering

Embedded Systems and Firmware Development
