# Fundamentals of Internet of Things — Firmware & Lab Archive

Embedded C firmware, circuit pinouts, and full-stack IoT implementations for **25CS2741 Fundamentals of Internet of Things + Lab**, organized into bare-metal **AT89S52 (8051)** peripheral programming (`8051/`) and **STM32 (Blue Pill & NUCLEO-F401RE)** connected edge nodes (`stm32/`) with **ESP8266**, **BME280**, and **Node-RED**.

---

## Repository Navigation

* **[`8051/`](8051)** — Keil C51 bare-metal projects, pinout diagrams, and per-task documentation for AT89S52 (CAT 2 – CAT 7).
* **[`stm32/`](stm32)** — STM32CubeMX & Keil MDK HAL projects for STM32F103 / NUCLEO-F401RE, ESP8266 Wi-Fi networking, BME280 sensing, and Node-RED flows (CAT 8 – CAT 15).

---

## Part I — AT89S52 (8051) Bare-Metal Firmware ([`8051/`](8051))

Built in **Keil C51** on an **11.0592 MHz AT89S52** using direct Special Function Register (SFR) access without external libraries:

* **Evaluation 2 — [`CAT2/TASK2B`](8051/CAT2/TASK2B)** ([README](8051/CAT2/TASK2B/README.md) · [Diagram](8051/CAT2/TASK2B/cat2b.png)): Direct `P1.1` SFR bit-addressing and calibrated 1 Hz LED blink loop.
* **Evaluation 3 — [`CAT3/TASK3A`](8051/CAT3/TASK3A)** ([README](8051/CAT3/TASK3A/README.md) · [Diagram](8051/CAT3/TASK3A/cat3a.png)): Active-low port masking, 20 ms release-edge switch debouncing, and 4-mode LED FSM.
* **Evaluation 4 — [`CAT4/TASK4A`](8051/CAT4/TASK4A)** ([README](8051/CAT4/TASK4A/README.md) · [Diagram](8051/CAT4/TASK4A/cat4a.png)): Sequential row-scan 4×4 keypad decoder, open-drain Port 0 7-segment driver (10 kΩ pull-ups), and LED mode controller.
* **Evaluation 5 — [`CAT5`](8051/CAT5)** ([`TASK5A`](8051/CAT5/TASK5A/README.md) · [`TASK5B`](8051/CAT5/TASK5B) · [`TASK5C`](8051/CAT5/TASK5C/README.md)): Timer 0 Mode 1 ISRs for 1 s periodic toggling, 1 kHz software PWM fading, 100 Hz–5 kHz square waves, multi-waveform bitstream generation, and ULN2003 unipolar stepper motor scheduling.
* **Evaluation 6 — [`CAT6`](8051/CAT6)**: Timer 1 auto-reload 9600-8-N-1 UART transmission and Serial ISR (`0x0023`) full-duplex echo with a 32-byte RX ring buffer.
* **Evaluation 7 — [`CAT7`](8051/CAT7)**: 4-bit HD44780 LCD initialization, flicker-free DDRAM cursor updates, and port-isolated 2D keypad sprite navigation.

---

## Part II — STM32, ESP8266 & Cloud IoT Stack ([`stm32/`](stm32))

Built with **STM32CubeMX**, **Keil MDK**, and **STM32 HAL** across STM32 Blue Pill and **NUCLEO-F401RE (Cortex-M4)** boards:

* **Evaluation 8 — [`CAT8`](stm32/CAT8) (STM32 GPIO & Non-Blocking Press Classifier):** Switch-following LED (`8A`), debounced stateful toggle (`8B`), and `HAL_GetTick()` duration classifier distinguishing short press (`< 1 s`, toggle) from long press (`≥ 1 s`, continuous blink mode) without blocking delays (`8C`).
* **Evaluation 9 — [`CAT9`](stm32/CAT9) (STM32 UART Command Interface):** Serial TX/RX echo (`9A`), `\r`/`\n` line-ending framing analysis in PuTTY, and string command parser controlling the onboard LED via `LED ON`, `LED OFF`, and `LED TOGGLE` (`9B`).
* **Evaluation 10 — [`CAT10`](stm32/CAT10) (STM32–Wemos D1 Mini Wi-Fi Interface):** Dual-UART bridge connecting STM32 to ESP8266 and PC terminal, AT command diagnostics (`AT`, `AT+GMR`, `AT+CWMODE`, `AT+CWLAP`, `AT+CIFSR`), and Wi-Fi station association via `AT+CWJAP`.
* **Evaluation 11 — [`CAT11`](stm32/CAT11) (Embedded HTTP Server & Node-RED Client):** Multi-connection TCP server (`AT+CIPMUX=1`, `AT+CIPSERVER=1,80`), `+IPD` HTTP request parsing, two-step `AT+CIPSEND` HTML response framing, and Node-RED HTTP Request flow integration.
* **Evaluation 12 — [`CAT12`](stm32/CAT12) (NUCLEO-F401RE Cortex-M4 Input Control):** Clock tree and hardware bring-up on STM32F401RE, fixed-interval LED blink, stateful push-button toggle, and short-press vs. long-press action dispatch.
* **Evaluation 13 — [`CAT13/TASK13`](stm32/CAT13/TASK13) (BME280 I2C Sensing & HTTP JSON Telemetry):** Bosch Sensortec BME280 Sensor API integration (`bme280.c`) over `I2C1` (`0x76`, chip ID `0xD0`), compensated temperature/pressure/humidity readout, dynamic JSON HTTP responses with exact `Content-Length`, and Node-RED min/max/average statistics.
* **Evaluation 14 — [`CAT14/TASK14`](stm32/CAT14/TASK14) (BME280 MQTT Telemetry & Node-RED Dashboard):** Custom `ESPLib` MQTT client connecting to `broker.emqx.io:1883`, `SysTick_Handler` `MQTTTimer()` scheduling, and live JSON sensor publishing (`MQTT_publishTopic`) visualized in Node-RED.
* **Evaluation 15 — [`CAT15/TASK15`](stm32/CAT15/TASK15):** Extended STM32 IoT lab implementation.

---

## Toolchains & Hardware Stack

* **MCUs & Modules:** AT89S52 (11.0592 MHz), STM32 Blue Pill, STM32 NUCLEO-F401RE, Wemos D1 Mini (ESP8266), Bosch BME280 (I2C), ULN2003 + Unipolar Stepper, HD44780 16×2 LCD, 4×4 Matrix Keypad.
* **IDEs & Tools:** Keil uVision C51, STM32CubeMX, Keil MDK-ARM, PuTTY / Tera Term, Node-RED, Mosquitto / EMQX Public MQTT Broker.
