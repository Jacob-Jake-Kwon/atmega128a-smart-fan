# ATmega128A Smart Fan Controller

An embedded smart fan controller developed using the ATmega128A microcontroller.

The system supports:

- IR Remote Control (NEC Protocol)
- Multi-Speed PWM Fan Control
- Servo-Based Oscillation (Sweep Mode)
- Countdown Timer
- I2C LCD Status Display
- Physical Button Controls
- Real-Time Interrupt Processing

---

## Features

### Fan Speed Control

Three fan speed levels are available:

| Speed | PWM Duty |
|---------|---------|
| Low | 2999 |
| Medium | 3999 |
| High | 4998 |

Users can control speed using:

- Physical Push Button
- IR Remote

---

### Oscillation (Sweep Mode)

A servo motor automatically sweeps left and right.

Features:

- Toggle ON/OFF
- Servo angle tracking
- Smooth oscillation movement

---

### Timer Function

Users can configure a shutdown timer through the IR remote.

Functions:

- Increase Timer
- Decrease Timer
- Start Timer
- Pause Timer
- Cancel Timer

When the timer reaches zero:

- Fan automatically turns OFF
- Servo stops
- LCD updates status

---

### I2C LCD Interface

16x2 LCD connected through a PCF8574 I2C backpack.

Displayed Information:

```text
Spd:2 Swp:ON

Run:15:23
```

---

### IR Remote Control

The system decodes NEC infrared protocol using:

- External Interrupt INT4
- Timer1 Pulse Measurement

Supported Commands:

| Remote Button | Function |
|---------------|------------|
| + | Timer Increase |
| - | Timer Decrease |
| Play/Pause | Start/Pause Timer |
| Speed 1 | Low Speed |
| Speed 2 | Medium Speed |
| Speed 3 | High Speed |
| Sweep | Toggle Oscillation |
| OFF | Shutdown |

---

## Hardware

### Microcontroller

- ATmega128A
- 16 MHz Clock

### Components

- DC Fan Motor
- SG90 Servo Motor
- IR Receiver Module
- IR Remote Controller
- 16x2 LCD
- PCF8574 I2C Backpack
- Push Buttons
- 2N2222A Transistor
- 1N4001 Flyback Diode
- 1kΩ Base Resistor

---

## Pin Mapping

| Device | Pin |
|----------|------|
| IR Receiver | PE4 (INT4) |
| Fan PWM | PE3 (OC3A) |
| Servo PWM | PE5 (OC3C) |
| Fan Button | PG3 |
| Sweep Button | PG4 |
| I2C SCL | PD0 |
| I2C SDA | PD1 |

---

## System Architecture

```text
IR Remote
     │
     ▼
IR Receiver (INT4)
     │
     ▼
ATmega128A
 ├── PWM Fan Control
 ├── Servo Sweep Control
 ├── Timer Scheduler
 └── I2C LCD Driver
```

---

## Software Architecture

```text
main.c
│
├── Button Handler
├── IR Decoder
├── Timer Manager
├── Servo Controller
├── Fan Speed Controller
└── LCD Interface
```

---

## Project Highlights

### Interrupt-Based IR Decoder

NEC protocol decoding implemented using:

- INT4 External Interrupt
- Timer1 Pulse Timing Measurement

This allows accurate decoding while maintaining responsive fan control.

---

### Non-Blocking System Design

The firmware avoids large blocking loops and instead uses:

- State Variables
- Periodic Updates
- Event-Driven Processing

This enables:

- Responsive remote input
- Smooth servo movement
- Accurate timer countdown

---

### I2C LCD Driver

Custom 4-bit LCD driver implemented over PCF8574 I2C backpack.

Key capabilities:

- Character output
- Cursor positioning
- Backlight control
- Command transmission

---

## Demonstration

Features demonstrated:

- Remote fan speed adjustment
- Oscillation control
- Timer scheduling
- Automatic shutdown
- LCD monitoring

---

## Future Improvements

- EEPROM Settings Storage
- Temperature Sensor Integration
- Automatic Fan Speed Adjustment
- Bluetooth Control
- Mobile App Interface

---

## Author

Jacob Kwon

Embedded Systems Project  
ATmega128A | AVR C | PWM | Interrupts | I2C | Servo Control
