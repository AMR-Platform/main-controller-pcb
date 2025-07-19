# Custom Controller Board

> **Overview**  
> A compact, USB-C–enabled controller board built around the ATmega32U4 MCU for dual-axis stepper motor control with encoder feedback, sensor integration, and flexible communication interfaces.


## Features

- **Microcontroller**: ATmega32U4 (44-pin TQFP) with native USB support  
- **Power**: USB-C or external 5V supply with automatic source selection  
- **Motor Control**:  
  - Two PUL/DIR/EN outputs for CL57T V4.1 stepper drivers  
  - Differential encoder inputs via SN75157DR line receivers  
- **Sensors**:  
  - I²C interface to Adafruit BNO055 9-DOF IMU  
  - Three analog cliff sensors  
  - Dual-channel battery voltage monitoring  
- **Communication & Debug**:  
  - USB-C (full-speed USB 2.0)  
  - SPI programming header  
  - 10-pin JTAG header  
- **User Interface**: Status LEDs and push-button inputs  
- **Signal Integrity**: Controlled-impedance differential routing, proper termination, ground planes


---
# Technical Challenges

## Encoder Signal Acquisition for MCU Integration
Industrial environments are electrically noisy; stepper motors and long cables can introduce substantial electromagnetic interference, leading to false encoder readings, glitches, and motor missteps.


- **Solution**:
  - Utilize dedicated buffer ic  for splitting encoder signals, which offer high input impedance and proper conversion to logic-level signals for MCUs without loading or distorting the encoder output
  - Avoid single-ended buffers, preventing signal integrity issues and logic contention
  - Employ differential receivers (SN75157) to reject common-mode noise before signals reach the MCU, ensuring robust, error-free pulse counting.


## License

This project is licensed under the [MIT License](LICENSE).

