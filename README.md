# Meshtastic Flasher (BLE)

A BLE flasher for Meshtastic devices.

Supports flashing firmware via bluetooth in a web browser.

> NOTE: Your web browser must support [Web Bluetooth](https://caniuse.com/web-bluetooth)

## How to flash?

- Open `index.html` in your web browser.
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

Alternatively, you could use the Meshtastic [python cli](https://github.com/meshtastic/python).

```
liamcottle@Liams-MacBook-Pro ~ % meshtastic --ble-scan
Found: name='LIAM_c088' address='CAECB11E-9D01-40FE-7BC0-04CA47DD6E0B'
BLE scan finished
```

```
liamcottle@Liams-MacBook-Pro ~ % meshtastic --ble LIAM_c088 --reboot-ota
Connected to radio
INFO file:node.py rebootOTA line:563 Telling node to reboot to OTA in 10 seconds
```

Your node will reboot into OTA mode and you can then flash via the web ui.

> NOTE: You may want to set a fixed pin for bluetooth as you will be prompted for the pin if your device hasn't been paired before. This is less secure than a random pin, but you wouldn't be able to see it on the screen if the device is not easily accessible physically.

## Why do I need this?

I have several Meshtastic devices that can't easily be connected to via USB for flashing via the official Meshtastic web flasher.

However, I am able to connect to them directly via bluetooth.

This project makes it easier to update the firmware over BLE using my MacBook without needing to take the nodes out of their enclosures nor connect to them via USB.

## Supported Devices

I have successfully flashed the following devices and firmwares over BLE.

**Heltec v3**

- [firmware-heltec-v3-2.2.18.e9bde80-update.bin](https://github.com/meshtastic/meshtastic.github.io/blob/master/firmware-2.2.18.e9bde80/firmware-heltec-v3-2.2.18.e9bde80-update.bin)
- [firmware-heltec-v3-2.3.3.8187fa7-update.bin](https://github.com/meshtastic/meshtastic.github.io/blob/master/firmware-2.3.3.8187fa7/firmware-heltec-v3-2.3.3.8187fa7-update.bin)

## TODO

- Add support for connecting to a Meshtastic device over BLE to send the Reboot OTA admin message.
- Add support for downloading firmware files directly from GitHub, like the [official web flasher](https://flasher.meshtastic.org/).

## References

- https://meshtastic.discourse.group/t/ota-firmware-update-esp32-based-modules/10311
- https://github.com/garthvh/Meshtastic-Flasher-OTA-ESP32/blob/main/MeshtasticFlasher/BLEConnection.swift
- https://github.com/meshtastic/firmware-ota/blob/33451a5c690a2366e292be194863c877560e86d0/src/main.cpp
