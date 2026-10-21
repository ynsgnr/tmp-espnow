# Nous A8T plug-to-plug trigger (ESPHome + ESP-NOW)

Plug A (sensor) detects power draw and sends an ESP-NOW packet to plug B,
which switches on for 30 minutes and then off. No router needed.

Pins come from the Tasmota template of the A8T:
relay GPIO15, button GPIO4, LED GPIO2 (inverted), BL0937: SEL GPIO16,
CF1 GPIO34, CF GPIO35.
The CF/CF1 assignment and SEL polarity are inferred from the template
and unverified. If the reading is wrong, swap the two pins or toggle `inverted`.

## Build
    pip install esphome
    esphome compile esphome/a8t-sensor.yaml
    esphome compile esphome/a8t-receiver.yaml

Set `peer_mac` in `a8t-sensor.yaml` to plug B's MAC first.
Flash `firmware.factory.bin` over serial (plug disconnected from mains).
There is no wifi/OTA in these configs, so later updates also need serial.
