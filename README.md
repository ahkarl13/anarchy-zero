# Anarchy Zero

An open-source, open-hardware alternative to the Flipper Zero. More powerful silicon, built-in Wi-Fi, color IPS display, and RGB LEDs that shine through a translucent case — at half the price.

> **Status:** 🟡 KiCad schematic v0.1 complete. PCB layout in progress.
> **License:** CERN-OHL-S v2 (hardware) · MIT (firmware)

---

## Core specs

| Component | Part | Notes |
|-----------|------|-------|
| MCU | ESP32-S3-WROOM-1-N16R8 | 240 MHz dual-core, 16 MB flash, 8 MB PSRAM, Wi-Fi + BT built-in |
| Sub-GHz | TI CC1101 (QFN-20) | Same chip as Flipper → community `.sub` file compatibility |
| NFC / RFID HF | NXP PN532 | 13.56 MHz · MIFARE · FeliCa |
| RFID LF | EM4095 | 125 kHz read/write |
| IR TX | 3× TSAL6400 + 2N7002 | Driven from RMT on IO5 |
| RGB LEDs | 8× WS2812B | Perimeter, shine through translucent case |
| Display | 1.54" IPS 240×240 ST7789 | **Color** — vs Flipper's mono 128×64 |
| Battery | 2500 mAh LiPo | ~30 day standby target |
| GPIO header | 2×9 2.54 mm | **Flipper Zero addon-board compatible** (hard requirement) |

## Differences vs Flipper Zero

| Feature | Anarchy Zero | Flipper Zero |
|---------|--------------|--------------|
| CPU | ESP32-S3 240 MHz dual-core | STM32WB55 64 MHz single-core |
| Flash | 16 MB | 1 MB |
| Wi-Fi | ✅ Built-in | ❌ $30 addon |
| Display | Color IPS | Monochrome |
| RGB LEDs | 8× perimeter | None |
| PSRAM | 8 MB | None |
| Price target | $99 | $199 |
| License | CERN-OHL-S v2 open | Closed |

## Firmware stack (planned)

| Layer | Choice |
|-------|--------|
| RTOS | FreeRTOS via ESP-IDF |
| Language | C / C++ |
| GUI | LVGL 9.x |
| OTA | ESP-IDF OTA over Wi-Fi (no PC needed) |
| Companion app | Flutter (iOS + Android) |

## Roadmap

| Phase | Weeks | Deliverables |
|-------|-------|--------------|
| 1 — Hardware | 1–4 | KiCad schematic → PCB layout → JLCPCB proto |
| 2 — Firmware core | 5–8 | HAL, FreeRTOS tasks, GUI, SD storage |
| 3 — Radio apps | 9–14 | Sub-GHz, NFC/RFID, IR, iButton, BadUSB |
| 4 — Wi-Fi + BT | 15–18 | Marauder Wi-Fi, BLE scanner, Mousejack |
| 5 — Ecosystem | 19–22 | Public release, docs, production run, website |

## RGB LED behavior modes

8 WS2812Bs on a 5 V VSYS rail, level-shifted through a 74HCT1G125 (IO4 3.3 V → 5 V DIN). 300 Ω series on DIN, 100 nF bypass per LED.

| Mode | Pattern |
|------|---------|
| Idle | Slow breathing cyan |
| Sub-GHz TX | Fast blue sweep |
| NFC read | Green rotating orbit |
| IR blast | White strobe |
| BadUSB | Rapid red flicker |
| Charging | Amber orbital chase |
| Error | Red double-blink |

## Repo layout (planned)

```
anarchy-zero/
├── hardware/        # KiCad schematic + PCB
├── firmware/        # ESP-IDF + LVGL
├── companion/       # Flutter mobile app
├── docs/            # Build guides, schematics
└── case/            # Fusion 360 / FreeCAD source
```

## Status & next steps

- [x] Schematic v0.1 drafted
- [ ] ERC clean pass
- [ ] PCB layout — RF ICs first, then perimeter LEDs
- [ ] Translucent case CAD (Fusion 360)
- [ ] Firmware HAL scaffold
- [ ] First JLCPCB proto run

## License

- **Hardware** — [CERN-OHL-S v2](https://ohwr.org/cern_ohl_s_v2.txt)
- **Firmware** — MIT
- **Documentation** — CC-BY-SA 4.0
