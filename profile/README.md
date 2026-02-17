# TrailCurrent

**An open-source Software Defined Vehicle platform built on edge-first autonomous intelligence.**

TrailCurrent is a complete, production-grade system architecture for intelligent vehicle and mobile platform management. From embedded microcontrollers on a CAN bus to cloud backends and mobile applications, TrailCurrent demonstrates how autonomous systems should work: local-first, offline-capable, and with data ownership in the hands of the user.

---

## Why TrailCurrent Exists

Most connected vehicle and IoT platforms assume persistent cloud connectivity. They ship your data upstream, process it remotely, and send decisions back down. This creates latency, privacy exposure, single points of failure, and a fundamental loss of control.

TrailCurrent takes the opposite approach:

- **Edge-first intelligence** -- Decisions happen locally, at the point of action, not in a distant data center.
- **Offline-capable by design** -- The system works without internet. Cloud is an enhancement, not a dependency.
- **Data sovereignty** -- Your telemetry, your sensors, your data. It stays with you unless you choose otherwise.
- **Full-stack transparency** -- Hardware schematics, firmware, gateway software, cloud services, and mobile apps are all open source.

---

## Architecture

See the [interactive architecture overview](https://trailcurrent.com/architecture.html) for a visual walkthrough of the full system.

TrailCurrent spans the full autonomous systems stack:

```
 Hardware Modules (ESP32 / ESP32-C6)
        |
     CAN Bus
        |
 Edge Gateway (MQTT / Docker / Node.js)
        |
     Cloud Backend (Node.js / PostgreSQL)
        |
     Mobile App (Kotlin / Jetpack Compose)
```

### Hardware & Firmware

Custom PCBs designed in KiCAD with ESP32-based firmware written in C++ using PlatformIO. Modules communicate over CAN bus and ESP-NOW wireless, covering:

- Vehicle power distribution and monitoring
- GNSS positioning
- Air quality sensing
- Trailer monitoring (seven-pin interface, leveling, shunt current)
- MPPT solar charge controller integration
- Cabinet and door sensors
- Multi-button control panels
- Wall-mounted and in-vehicle displays

### Edge Gateway

A Dockerized compute platform that runs inside the vehicle. Aggregates sensor data via MQTT, serves local dashboards with offline map tiles, and synchronizes selectively with cloud services when connectivity is available.

### Cloud & Mobile

A Node.js backend with PostgreSQL for optional remote access and fleet-level visibility. A native Android application built with Kotlin and Jetpack Compose provides real-time monitoring and control.

---

## Repository Organization

Repositories are organized across two organizations:

### Core Infrastructure & Libraries

| Repository | Description |
|---|---|
| **[InVehicleCompute](https://github.com/trailcurrentoss/TrailCurrentInVehicleCompute)** | Dockerized edge gateway with MQTT broker, tile server, and local dashboards |
| **[PowerDistributionModule](https://github.com/trailcurrentoss/TrailCurrentPowerDistributionModule)** | Vehicle power management hardware and firmware |
| **[KiCADLibraries](https://github.com/trailcurrentoss/TrailCurrentKiCADLibraries)** | Shared schematic symbols, PCB footprints, and 3D models |
| **[Documentation](https://github.com/trailcurrentoss/TrailCurrentDocumentation)** | Architecture guides, setup instructions, and design decisions |
| **[OtaUpdateLibraryWROOM32](https://github.com/trailcurrentoss/OtaUpdateLibraryWROOM32)** | Over-the-air firmware update library for ESP32 WROOM-32 |
| **[TwaiTaskBasedLibraryWROOM32](https://github.com/trailcurrentoss/TwaiTaskBasedLibraryWROOM32)** | FreeRTOS task-based CAN (TWAI) driver for ESP32 |
| **[ESP32ArduinoDebugLibrary](https://github.com/trailcurrentoss/ESP32ArduinoDebugLibrary)** | Debugging utilities for ESP32 Arduino development |
| **[Esp32C6OtaUpdateLibrary](https://github.com/trailcurrentoss/Esp32C6OtaUpdateLibrary)** | Over-the-air firmware update library for ESP32-C6 |
| **[Esp32C6TwaiTaskBasedLibrary](https://github.com/trailcurrentoss/Esp32C6TwaiTaskBasedLibrary)** | FreeRTOS task-based CAN (TWAI) driver for ESP32-C6 |
| **[C6SuperMiniRgbLedLibrary](https://github.com/trailcurrentoss/C6SuperMiniRgbLedLibrary)** | RGB LED status indicator driver for ESP32-C6 Super Mini |

### Application Layer

| Repository | Description |
|---|---|
| **[CanEspNowGateway](https://github.com/trailcurrentoss/TrailCurrentCanEspNowGateway)** | CAN bus to ESP-NOW wireless bridge |
| **[GnssModule](https://github.com/trailcurrentoss/TrailCurrentGnssModule)** | GPS/GNSS positioning module firmware |
| **[AirQualityModule](https://github.com/trailcurrentoss/TrailCurrentAirQualityModule)** | Environmental air quality sensor firmware |
| **[BtGateway](https://github.com/trailcurrentoss/TrailCurrentBtGateway)** | Bluetooth gateway for sensor aggregation |
| **[VehicleLeveler](https://github.com/trailcurrentoss/TrailCurrentVehicleLeveler)** | Accelerometer-based vehicle leveling system |
| **[ShuntGateway](https://github.com/trailcurrentoss/TrailCurrentShuntGateway)** | Current shunt monitoring for battery systems |
| **[SevenPinTrailerMonitor](https://github.com/trailcurrentoss/TrailCurrentSevenPinTrailerMonitor)** | Standard trailer connector monitoring |
| **[MpptCanGateway](https://github.com/trailcurrentoss/TrailCurrentMpptCanGateway)** | Solar charge controller CAN integration |
| **[CabinetAndDoorSensor](https://github.com/trailcurrentoss/TrailCurrentCabinetAndDoorSensor)** | Magnetic reed switch monitoring |
| **[EightButtonPanel](https://github.com/trailcurrentoss/TrailCurrentEightButtonPanel)** | Multi-function control panel hardware and firmware |
| **[ElectricHeaterControl](https://github.com/trailcurrentoss/TrailCurrentElectricHeaterControl)** | Heater control system hardware and firmware |
| **[InVehicleTrailerMonitoring](https://github.com/trailcurrentoss/TrailCurrentInVehicleTrailerMonitoring)** | In-vehicle trailer monitoring display firmware |
| **[TrailCurrentCloud](https://github.com/trailcurrentoss/TrailCurrentCloud)** | Cloud backend services |
| **[TrailCurrentAndroidApp](https://github.com/trailcurrentoss/TrailCurrentAndroidApp)** | Native Android monitoring and control application |
| **[WaveshareEsp32s3Remote](https://github.com/trailcurrentoss/TrailCurrentWaveshareEsp32s3Remote)** | ESP32-S3 4.3" touchscreen remote control |
| **[WallMountedDisplay](https://github.com/trailcurrentoss/TrailCurrentWallMountedDisplay)** | Wall-mounted status display |
| **[WallMountedDisplaySunton7Inch](https://github.com/trailcurrentoss/TrailCurrentWallMountedDisplaySunton7Inch)** | 7-inch Sunton wall-mounted display |

---

## Technical Principles

**Modular by default.** Each module is an independent unit with its own firmware, communicating over standardized protocols. Swap, add, or remove modules without redesigning the system.

**Hardware meets software rigor.** PCB designs, firmware, and cloud services all follow the same standards: version controlled, documented, and reproducible.

**No vendor lock-in.** Standard protocols (CAN bus, MQTT, HTTP), commodity hardware (ESP32), and open-source tooling (KiCAD, PlatformIO, Docker) throughout.

**Security as a constraint, not an afterthought.** Secrets management, OTA update verification, and transport encryption are built into the architecture from the start.

---

## Getting Started

Each repository includes its own README with setup instructions. For a system-level overview, start with the **Documentation** repository. For the edge computing platform, see **InVehicleCompute**. For hardware designs, browse the individual module repositories and reference **KiCADLibraries** for shared assets.

### Prerequisites

- **Firmware development:** PlatformIO, ESP-IDF toolchain
- **Edge gateway:** Docker, Docker Compose
- **Cloud services:** Node.js, PostgreSQL
- **Hardware design:** KiCAD 8+
- **Mobile app:** Android Studio, Kotlin

---

## Contributing

Contributions are welcome. Whether it's improving documentation, fixing bugs, adding features, or designing new hardware modules, open an issue or submit a pull request.

---

## License

Individual repositories specify their own licenses. See each repository's LICENSE file for details.
