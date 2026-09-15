# Sensors Board — Task 10.2

## What it does

Four things get read and sent to the STM32:
- **Motion & orientation** — MPU6050 (raw accel/gyro) + BNO055 (does its own sensor fusion onboard)
- **Distance** — HC-SR04 ultrasonic
- **Endpoint detection** — a limit switch, cleaned up with a debounce circuit

Everything else on the board (ESD protection, decoupling caps, bulk cap) exists to keep those readings clean — protecting against static shocks, power spikes, and mechanical switch noise.

## Key decisions

- **BNO055 over the cheaper generic clone** — no verified CAD library existed for the clone anywhere; design certainty mattered more than saving cost
- **BNO055 address: 0x28**, ADR pin deliberately tied to GND (the alternative address, not the 0x29 default) — chosen over leaving it floating, since floating digital pins have undefined behavior
- **HC-SR04 Echo pin** goes through a 1kΩ/2kΩ voltage divider — it outputs 5V, our logic runs 3.3V
- **Debounce circuit (10kΩ + 100nF)** — calculated from a target ~1ms time constant against a 10ms worst-case switch bounce
- **ESD IC (USBLC6-2SC6)** — chosen for low capacitance (2.5pF) so it doesn't degrade the I2C signal; placed right at the connector per its own datasheet's layout guidance

## Files

Schematic, PCB layout, component libraries, and `Task10.2-Sensors_BOM.xlsx` (real supplier links, EGP pricing, working totals).
