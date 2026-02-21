# UART-Based LED Matrix Visualization System  
Communication Synchronization & Real-Time Display Stabilization

Real-time environmental data visualization system using CircuitPython and RGB LED Matrix panels.  
This project focuses on troubleshooting asynchronous UART communication, protocol synchronization between two microcontrollers, and memory-aware display optimization.

---

## System Overview

**Architecture**

Sensor MCU (Arduino Nano)  
→ UART Transmission  
→ Metro M4 (CircuitPython)  
→ RGB LED Matrix Panels (128x32)

The system receives structured sensor data over serial communication and renders it in real time on chained LED panels.

---

## Initial Problem

The LED panels powered correctly but displayed nothing.

Hardware debugging confirmed:

- TX voltage stable at 3.3V  
- Supply voltage stable (~4V measured)  
- No grounding issues  
- Shield and panel wiring correct  

The issue was not electrical.  
The failure originated from UART data handling logic.

---

## Root Cause

The original implementation immediately parsed incoming UART data:

```python
data_list = data_string.split(",")
```

Since UART is asynchronous, data often arrives in incomplete fragments.

Example of partial packet:

25.3,45.2,PM2.
