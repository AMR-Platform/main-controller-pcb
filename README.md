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
## Technical Challenges

Designing this custom controller board involved overcoming several critical technical challenges:

**Encoder Signal Acquisition for MCU Integration**

Industrial environments are electrically noisy, stepper motors and long cables can introduce substantial electromagnetic interference, leading to false encoder readings, glitches, and motor missteps.

- **Solution**:
  - Utilize dedicated buffer ic  for splitting encoder signals, which offer high input impedance and proper conversion to logic-level signals for MCUs without loading or distorting the encoder output
  - Avoid single-ended buffers, preventing signal integrity issues and logic contention
  - Employ differential receivers (SN75157) to reject common-mode noise before signals reach the MCU, ensuring robust, error-free pulse counting.

 **High-Speed Differential Signal Integrity**  
   - Controlled-impedance routing (90–120 Ω) for encoder A+/A– and B+/B– pairs  
   - Length matching within ±0.1 mm to prevent skew   
   - Avoided sharp bends and stubs; routed over continuous ground plane  

**Mixed-Signal Noise Isolation**  
   - Physical separation of analog (cliff sensors, battery monitors) and noisy digital/motor control traces  
   - Dedicated ground planes and star-point connections for analog vs. digital returns  
   - Shielded, twisted-pair encoder cables with chassis-grounded shields  

**USB-C Integration & Protection**  
   - Matched-length differential pair routing on D+/D–  
   - CC1/CC2 pull-down resistors (5.1 kΩ) for UFP detection  
   - ESD suppressors 
   - UVCC/UCAP decoupling (0.1 µF + 1 µF) for internal USB regulator stability  

**Reliable Power Source Selection**  
   - Power selection header between USB-C VBUS and external 5 V input to prevent backfeed  
   - Resettable fuse and bulk decoupling on both power sources  
   - Voltage divider and filter network for 5 V VBUS sensing at MCU’s VBUS pin  

**Firmware Programming & Debug Accessibility**  
   - Standard 10-pin SPI header and 10-pin JTAG header with clear silkscreen labels  
   - Test points for USB D+/D–, SPI lines, and key analog nets  
   - Buffer footprints for optional level-shifting or signal conditioning  

**User Interface Debouncing & Visibility**  
   - Software-debounced GPIO inputs for push buttons; optional RC filter footprint  
   - Active-low LED indicators with 330 Ω current-limiting resistors   

**Compact, Manufacturable Layout**  
   - Hierarchical schematic blocks for modularity and maintainability  
   - Strategic component placement: MCU centered, connectors at edges, decoupling caps adjacent to IC power pins  
   - 2-layer PCB stack-up for noise control and routing efficiency  


## License

This project is licensed under the [MIT License](LICENSE).

