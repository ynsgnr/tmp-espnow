# Nous A8T plug-to-plug trigger (ESPHome + ESP-NOW)

Plug A (sensor) detects power draw and sends an ESP-NOW packet to plug B,
which switches on for 30 minutes and then off.

Pins from the A8T Tasmota template (checked against Tasmota's ESP32
source): relay GPIO13, button GPIO4, LED GPIO2 (inverted), BL0937 SEL
GPIO14 (inverted), CF1 GPIO26, CF GPIO27.

## Migrate over the air (no opening the plug)
Follow https://esphome.io/guides/migrate_sonoff_tasmota/ :
1. `cp esphome/secrets.yaml.example esphome/secrets.yaml`, fill in WiFi.
   Set `peer_mac` in a8t-sensor.yaml to plug B's MAC.
2. `esphome compile esphome/a8t-receiver.yaml`, then upload `firmware.bin`
   via Tasmota Firmware Upgrade -> Upgrade by file.
3. Migrate the partition table (`esphome upload --partition-table ...`)
   using the method that fits the "Used size" in the logs.
4. Remove `allow_partition_access`, reflash normally.
Power loss during step 3 can brick the plug (serial needed to recover).
