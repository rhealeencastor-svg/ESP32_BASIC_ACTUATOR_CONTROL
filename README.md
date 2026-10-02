# Laboratory Activity 6: Basic Actuator Control

**Name:** Rhea Leen Castor  
**Course:** BCA188 – Programming for Internet of Things  

## Objective

To control a DC motor using an ESP32-WROOM, push button, and motor driver.

The push button controls whether the motor runs or coasts.

---

## Materials Used

- ESP32-WROOM Development Board (USB Type-C)
- USB Type-C Data Cable
- DC Motor
- Motor Driver Breakout Board
- Push Button
- Breadboard
- Jumper Wires
- External Motor Power Supply

---

## Circuit Wiring

### Push Button

| Connection | ESP32 Connection |
| :--- | :--- |
| One side | GPIO23 |
| Other side | GND |

The button uses `INPUT_PULLUP`.

- Released = HIGH
- Pressed = LOW

### Motor Driver

| Driver Pin | ESP32 / Circuit Connection | Purpose |
| :--- | :--- | :--- |
| AIN1 | GPIO21 | Motor control input |
| AIN2 | GPIO22 | Motor control input |
| nSLEEP | GPIO27 | Enables the motor driver |
| VM | External motor power supply | Motor power |
| GND | ESP32 GND and power supply GND | Common ground |
| AOUT1 | Motor terminal | Motor output |
| AOUT2 | Motor terminal | Motor output |

---

## Circuit Connection

```text
ESP32 GPIO23 ─── Push Button ─── GND

ESP32 GPIO21 ─── AIN1
ESP32 GPIO22 ─── AIN2
ESP32 GPIO27 ─── nSLEEP

External Supply (+) ─── VM
External Supply (-) ─── GND
ESP32 GND ───────────── GND

AOUT1 ─── DC Motor ─── AOUT2
```

The ESP32 and motor power supply share a common ground.

---

## Inputs and Outputs

| Type | Device | Connection | Function |
| :--- | :--- | :--- | :--- |
| Input | Push Button | GPIO23 | Controls motor run/coast |
| Output | AIN1 | GPIO21 | Motor control |
| Output | AIN2 | GPIO22 | Motor control |
| Output | nSLEEP | GPIO27 | Enables the motor driver |
| Output | DC Motor | AOUT1 and AOUT2 | Mechanical output |

---

## Motor Information

| Specification | Value |
| :--- | :--- |
| Motor Model |  |
| Rated Voltage |  |
| Stall Current |  |
| Datasheet |  |

---

## Motor Driver Information

| Specification | Value |
| :--- | :--- |
| Breakout Model |  |
| Motor Supply Voltage Range |  |
| Output Current Limit |  |
| Datasheet |  |

---

## Driver Pin Functions

### AIN1

`AIN1` is used as the main control input for the motor in this activity.

When the button is pressed, GPIO21 sends HIGH to AIN1.

### AIN2

`AIN2` is kept LOW in the program.

Together with AIN1, it determines the motor output state.

### nSLEEP

`nSLEEP` enables the motor driver.

During setup, it is first set LOW and then changed to HIGH to wake the driver before the motor is controlled.

### VM

`VM` is the power input for the motor.

The motor receives power through the motor driver instead of directly from the ESP32.

### Common Ground

The ESP32, motor driver, and external motor power supply must share the same ground.

This allows the control signals from the ESP32 to have the same voltage reference as the motor driver.

---

## Program Operation

The push button is connected to GPIO23 and uses `INPUT_PULLUP`.

When the button is released:

```text
AIN1 = LOW
AIN2 = LOW
```

The motor is placed in the coast state.

When the button is pressed:

```text
AIN1 = HIGH
AIN2 = LOW
```

The driver is commanded to run the motor in one direction.

The `nSLEEP` pin is controlled by GPIO27 and is set HIGH after the driver wake-up delay.

---

## Expected Behavior

| Button State | AIN1 | AIN2 | Motor State |
| :--- | :---: | :---: | :--- |
| Released | LOW | LOW | Coast |
| Pressed | HIGH | LOW | Run |
| Released again | LOW | LOW | Coast |

---

## Test Record

| Test | Expected Behavior | Observed Behavior |
| :--- | :--- | :--- |
| Power on | Motor remains stopped |  |
| Button released | Motor is in coast state |  |
| Button pressed | Motor runs |  |
| Button released again | Motor returns to coast state |  |

---

## Documentation

### Circuit Setup

[Insert image here]

### ESP32 and Driver Connections

[Insert image here]

### Motor Connection

[Insert image here]

### Push Button Connection

[Insert image here]

### Hardware Testing

[Insert image here]
