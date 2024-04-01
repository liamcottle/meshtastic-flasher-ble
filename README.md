# Meshtastic Flasher (BLE)

A BLE flasher for Meshtastic devices.

Supports flashing firmware via bluetooth in a web browser.

## How to flash?

- Select firmware file.
- Reboot Meshtastic device into OTA mode.
- Flash the firmware.
- Device should reboot into new version when complete.

> NOTE: Use the firmware files ending with `-update.bin`.
> https://github.com/meshtastic/meshtastic.github.io/tree/master

If your device does not auto reboot after flashing, something probably went wrong.

At this time, the Meshtastic [firmware-ota](https://github.com/meshtastic/firmware-ota/blob/33451a5c690a2366e292be194863c877560e86d0/src/main.cpp) running on the device does not send any events over BLE to tell us if flashing was successful or if it failed.

## How to reboot to OTA mode?

The Meshtastic iOS app supports sending the Reboot OTA admin message.

`Settings > Firmware Updates > Send Reboot OTA`

## TODO

- Add support for connecting to a Meshtastic device over BLE to send the Reboot OTA admin message.
- Add support for downloading firmware files directly from GitHub, like the [official web flasher](https://flasher.meshtastic.org/).

## References

- https://meshtastic.discourse.group/t/ota-firmware-update-esp32-based-modules/10311
- https://github.com/garthvh/Meshtastic-Flasher-OTA-ESP32/blob/main/MeshtasticFlasher/BLEConnection.swift
- https://github.com/meshtastic/firmware-ota/blob/33451a5c690a2366e292be194863c877560e86d0/src/main.cpp
