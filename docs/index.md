---
title: Welcome
description:  J1772 EVSE firmware for ESP32 based devices 
hide:
  - navigation
---
![ESP32 EVSE](assets/logo-full.svg#only-light)
![ESP32 EVSE](assets/logo-full-dark.svg#only-dark)

J1772 EVSE firmware for ESP32 based devices.

![Build with ESP-IDF](https://github.com/dzurikmiroslav/esp32-evse/workflows/Build/badge.svg)
[![GitHub version](https://img.shields.io/github/release/dzurikmiroslav/esp32-evse.svg)](https://github.com/dzurikmiroslav/esp32-evse/releases/latest)
[![License](https://img.shields.io/github/license/dzurikmiroslav/esp32-evse.svg)](20-software/LICENSE.md)
[![GitHub Sponsors](https://img.shields.io/badge/donate-GitHub_Sponsors-blue)](https://github.com/sponsors/dzurikmiroslav)
[![Web installer](https://img.shields.io/badge/web-installer-green?style=flat&logo=googlechrome&logoColor=lightgrey)](installer.md)

## Key features
 - Hardware abstraction for device design
 - Responsive web-interface
 - OTA update
 - Integrated energy meter
 - REST API
 - WebDAV
 - [Modbus](https://github.com/dzurikmiroslav/esp32-evse/wiki/Modbus) (RS485, TCP)
 - [Lua scripting](https://github.com/dzurikmiroslav/esp32-evse/wiki/Lua)
 - [Nextion HMI](https://github.com/dzurikmiroslav/esp32-evse/wiki/Nextion)
 - [AT commands](https://github.com/dzurikmiroslav/esp32-evse/wiki/AT-commands)
 - Scheduler

### Web installer

Easy initial installation of esp32-evse firmware can be performed using your browser (currently Google Chrome or Microsoft Edge).

[Web installer](installer.md)

### Device definition method

_One firmware to rule them all._ Not really :-) one per device platform (ESP32, ESP32-S2...).

There is no need to compile the firmware for your EVSE design.
Source code ist not hardcoded to GPIOs or other hardware design features.
All code is written in ESP-IDF without additional mapping layer like Arduino.

All configuration is written outside firmware in configuration file named _board.yaml_ on dedicated partition.
For example, on following scheme is minimal EVSE circuit with ESP32 devkit.

![Minimal circuit](images/minimal-circuit.png)

For this circuit there is config file _board.yaml_, for more information's see [YAML schema](https://github.com/dzurikmiroslav/esp32-evse/tree/master/board-config).

```yaml
deviceName: ESP32 minimal EVSE

button:
  gpio: 0

pilot:
  gpio: 33
  adcChannel: 7
  levels: [2410, 2104, 1797, 1491, 265]

acRelay:
  gpios: [32]
```

### Web interface

Fully responsive web interface is accessible local network IP address on port 80.

Dashboard page

![Dashboard](images/web-dashboard.png) 

Settings page

![Settings](images/web-settings.png)

Mobile dashboard page

![Dashboard mobile](images/web-dashboard-mobile.png)

Check out the [build examples page](10-hardware/build-examples.md) to see the hardware in action.

## Donations

ESP32 EVSE firmware is free, but costs money to develop harware and time to develop software.
This gift to the developer would demonstrate your appreciation of this software & hardware and help its future development.

[![GitHub Sponsors](https://img.shields.io/badge/donate-GitHub_Sponsors-blue)](https://github.com/sponsors/dzurikmiroslav)
