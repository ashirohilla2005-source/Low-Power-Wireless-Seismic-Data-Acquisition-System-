🌍 Low-Power Wireless Seismic Data Acquisition System

An energy-efficient, high-resolution, wireless geophone-based sensing platform for seismic monitoring and vibration analysis.

<p align="center">
  <img src="https://img.shields.io/badge/Platform-ESP32--C3-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/ADC-24--Bit-green?style=for-the-badge" />
  <img src="https://img.shields.io/badge/PCB-4--Layer-orange?style=for-the-badge" />
  <img src="https://img.shields.io/badge/EDA-KiCad-purple?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Project-Embedded%20Systems-red?style=for-the-badge" />
</p>---

📌 Project Overview

This project focuses on the design of a low-power, wireless seismic data acquisition system using a geophone sensor. The system is designed to detect ground vibrations, acquire high-resolution analog signals, and transmit seismic data wirelessly while minimizing power consumption.

The proposed system integrates a precision analog front-end, a high-resolution ADC, an ultra-low-power microcontroller, signal conditioning circuitry, and a wireless communication interface.

A key feature of the design is its event-driven power management architecture, in which the microcontroller remains in deep-sleep mode during inactive periods and wakes up when seismic activity is detected by a low-power comparator.

The system aims to provide a compact, efficient, and scalable solution for applications such as seismic monitoring, earthquake detection, structural health monitoring, vibration analysis, and IoT-based sensing networks.

---

🎯 Objectives

- Design a low-power seismic sensing system for battery-operated applications.
- Acquire weak geophone signals with high precision.
- Implement a 24-bit analog-to-digital conversion system.
- Reduce power consumption using event-driven wake-up and deep-sleep operation.
- Implement analog signal conditioning and input protection.
- Design a compact 4-layer PCB with optimized analog and digital layout.
- Enable wireless data communication for remote monitoring.
- Improve signal integrity and system reliability.

---

⚙️ System Architecture

                 🌍 GEOPHONE SENSOR
                         │
                         ▼
              ┌─────────────────────┐
              │  RC Input Protection│
              │  & Signal Filtering │
              └─────────────────────┘
                         │
                         ▼
              ┌─────────────────────┐
              │ Butterworth Low-Pass│
              │       Filter        │
              └─────────────────────┘
                         │
             ┌───────────┴───────────┐
             │                       │
             ▼                       ▼
     ┌───────────────┐      ┌────────────────┐
     │ Low-Power     │      │ Analog Switch │
     │ Comparator    │      │               │
     └───────────────┘      └────────────────┘
             │                       │
             │ Wake-up Signal        ▼
             │               ┌────────────────┐
             └──────────────►│  MCP3561 ADC   │
                             │    24-Bit      │
                             └────────────────┘
                                      │ SPI
                                      ▼
                             ┌────────────────┐
                             │   ESP32-C3     │
                             │ Processing &   │
                             │ Wireless       │
                             └────────────────┘
                                      │
                                      ▼
                              📡 Wireless Data
                              Transmission

---

🔬 Key Features

Feature| Description
🌍 Seismic Sensing| Geophone-based ground vibration detection
⚡ Low-Power Architecture| Event-driven operation to minimize energy consumption
💤 Deep Sleep| ESP32-C3 remains in low-power sleep during inactive periods
📊 High-Resolution Acquisition| 24-bit MCP3561 Delta-Sigma ADC
🎯 Precision Reference| ADR4525 stable 2.5 V voltage reference
🔋 Power Management| MIC94345 ultra-low-power LDO regulator
🔍 Signal Conditioning| RC protection and Butterworth low-pass filtering
🚨 Event Detection| Low-power comparator-based wake-up mechanism
🔌 Analog Switching| ADC input controlled during acquisition
📡 Wireless Connectivity| Integrated wireless communication capability
🧩 Hardware Integration| Compact mixed-signal electronics design
🖥️ PCB Design| Four-layer PCB with analog/digital design considerations

---

🧠 Hardware Components

Component| Function| Purpose
ESP32-C3| Microcontroller| Processing, control, SPI communication, wireless connectivity, deep sleep
MCP3561| 24-bit ADC| High-resolution digitization of weak geophone signals
ADR4525| Precision voltage reference| Stable 2.5 V reference for accurate ADC measurements
MIC94345| Low-dropout regulator| Clean and stable 3.3 V power supply
Geophone| Seismic sensor| Converts ground vibrations into electrical signals
Low-Power Comparator| Event detection| Detects seismic activity and generates wake-up signals
Analog Switch| Signal control| Connects the analog signal to the ADC during acquisition
RC Network| Input protection| Limits transients and suppresses unwanted high-frequency components
Butterworth Filter| Signal conditioning| Attenuates high-frequency noise while preserving the required signal band
Li-Po Battery| Power source| Portable battery-powered operation

---

🔋 Low-Power Operation

The system uses an event-driven architecture to reduce unnecessary power consumption.

Operating Sequence

1. The geophone continuously senses ground vibrations.
2. The analog input passes through the protection and filtering stages.
3. The low-power comparator monitors the conditioned signal.
4. The ESP32-C3 remains in deep sleep during inactive periods.
5. When the signal exceeds the configured threshold, the comparator generates a wake-up signal.
6. The ESP32-C3 wakes up and enables the analog acquisition path.
7. The MCP3561 digitizes the seismic signal.
8. The acquired data is processed and transmitted wirelessly.
9. The system returns to its low-power state.

        ┌─────────────────────┐
        │     Deep Sleep      │
        └──────────┬──────────┘
                   │
                   ▼
        Seismic Activity Detected?
                   │
          ┌────────┴────────┐
          │                 │
         NO                YES
          │                 │
          ▼                 ▼
     Stay Asleep      Wake ESP32-C3
                            │
                            ▼
                    Enable Acquisition
                            │
                            ▼
                     Read MCP3561
                            │
                            ▼
                    Process Seismic Data
                            │
                            ▼
                    Wireless Transmission
                            │
                            ▼
                      Return to Sleep

---

📈 Signal Processing & Conditioning

The analog front-end is designed to protect sensitive electronics and improve the quality of the acquired seismic signals.

Signal Processing Stages

Stage| Purpose
RC Input Network| Transient suppression, current limiting, and initial filtering
Butterworth Low-Pass Filter| Reduces high-frequency noise
Comparator| Detects signals exceeding the configured threshold
Analog Switch| Controls the ADC signal path
MCP3561 ADC| Converts the analog signal into high-resolution digital data

The combination of input protection, filtering, and event detection helps improve signal reliability and reduce unnecessary system activation.

---

🛠️ PCB Design

The hardware was designed using KiCad, with emphasis on mixed-signal PCB design and signal integrity.

PCB Design Considerations

- Four-layer PCB architecture
- Dedicated ground and power planes
- Analog and digital circuit separation
- Short and optimized sensitive analog signal routing
- Careful ADC and voltage-reference placement
- Local decoupling capacitors
- Reduced electromagnetic interference
- Improved power distribution
- Design Rule Check (DRC)
- Component footprint verification
- PCB visualization and 3D inspection

---

💻 Tools & Technologies

Category| Technology
Microcontroller| ESP32-C3
Firmware Development| Arduino Framework / ESP-IDF
Hardware Design| KiCad
Analog Circuit Design| RC Networks, Butterworth Filters
Data Acquisition| MCP3561 24-bit ADC
Communication| SPI
Wireless Connectivity| Wi-Fi / BLE capabilities
Power Electronics| MIC94345 LDO
PCB Design| 4-Layer PCB
Embedded Systems| C/C++
Signal Processing| Analog Signal Conditioning

---

🎯 Applications

- 🌋 Earthquake and seismic monitoring
- 🏗️ Structural health monitoring
- 🏢 Building vibration analysis
- 🌍 Environmental monitoring
- ⛏️ Geophysical sensing
- 📡 Distributed IoT sensor networks
- 🔬 Scientific instrumentation
- 🚨 Vibration-based event detection

---

🚀 Future Improvements

- Real-time seismic waveform visualization
- Cloud-based monitoring dashboard
- LoRa-based long-range communication
- GPS-based timestamp synchronization
- Data logging using external storage
- Advanced digital signal processing
- Machine-learning-based seismic event classification
- Battery-life optimization and power profiling
- Multi-node distributed seismic monitoring network
- Remote configuration and firmware updates

---

⭐ Key Takeaway

This project demonstrates the integration of precision analog electronics, embedded firmware, low-power system design, wireless communication, and PCB engineering into a compact seismic sensing platform.

The central design philosophy is to detect meaningful events efficiently, acquire high-resolution signals accurately, and minimize power consumption during inactive periods.

---

<p align="center">⚡ Build Smart. Sense Precisely. Consume Less Power. 🌍

</p>
