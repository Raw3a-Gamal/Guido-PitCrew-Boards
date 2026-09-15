# 🏎️ Guido-PitCrew-Boards

Three PCB boards for Radiator Springs' pit crew robot, Guido — built to extend pistons and swing servo arms fast enough to change a tire before the competition even finishes their brake check.

## The three boards

| Board | Folder | Job |
|---|---|---|
| **10.1 Actuators** | `10.1-actuators/` | Drives the solenoid valve and servo motor — the muscles |
| **10.2 Sensors** | `10.2-sensors/` | Reads motion, orientation, distance, and endpoint detection — the senses |
| **10.3 Power Distribution** | `10.3-power/` | Takes 12V in, outputs regulated 5V/12V with protection circuits — the heart |

## What each board actually does

**Actuators (10.1):** solenoid valve driven through a ULN2003A darlington array, servo motor with overcurrent protection, connected via a header-mounted STM32F411 BlackPill.

**Sensors (10.2):** MPU6050 (raw motion) and BNO055 (fused orientation) sharing one I2C bus, HC-SR04 for distance, a limit switch with a calculated debounce circuit for endpoint detection, USBLC6-2SC6 ESD protection on the I2C lines, and decoupling/bulk capacitors throughout for power stability.

**Power (10.3):** buck converter stepping 12V down to a regulated 5V rail, with overvoltage, overcurrent, and reverse-polarity protection — feeding the other two boards.
