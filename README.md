# EspHome-Gree
DIY Gree Versati III modbus interface based on ESPHome
![Home Assistant UI](/gWgBYqcLsEN2S66OJ06bcFKo.jpg)

# prerequisites
- Home Assistant (HA)
- ESP32 with cp2101 [on amazon](https://www.amazon.nl/dp/B071P98VTG?ref_=cm_sw_r_mwn_dp_SBXP3Q2HR019KM7MCFVS&th=1&psc=1)
- RS485 module [on amazon](https://www.amazon.nl/dp/B07DN115BZ?ref_=cm_sw_r_mwn_dp_3SAQTGR00DE9YA1PEM5G)
- 4 wires (dupont jumper cables or other)
- gree modbus connector + 2 wire cable - i used cut spare cable from gree installation package
- usb adapter for powering the ESP32
- cp2101 windows driver (https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers)
- ESP32 flashtool (https://www.espressif.com/en/support/download/other-tools)

# part 1 flash ESP with ESPHome custom firmware
- goto HA EspHome addon and choose to create a new Device. Don't connect ESP32 yet. Fill in details and create custom firmware and download the binary file.
- install the latest cp2101 windows driver
- To flash the custom firmware, ESP32 should be set to Firmware Download mode. This can be done either by the flash tool automatically, or by holding down the Boot button and tapping the EN button. After flashing binary files, the Flash Download Tool restarts your ESP32 module and boots the flashed application by default.
- use flashtool to flash the downloaded firmware file
- When flashing was succesful the ESP device should be visible in the ESPHome addon in Home Assistant
# part 2 hardware wiring
Wire the components according to the table below
|Esp32 pin|RS485 pin|Gree modbus connector|
|--------|----------|---------------|
|Gnd|Gnd||
|3V3|VCC||
|GIO16|RXD||
|GIO17|TXD||
||A|A|
||B|B|
**Make sure to place a 120 ohms resistor across the A and B pins to terminate the modbus serial line correctly.**
# part 3 update configuration.yaml
In part 1 a basic ESPHome firmware was flashed, which does not contain any code for managing the modbus connection. Now we are going to change that by adding the additional yaml configuration to the configurarion.yaml of the device in ESPHome and let ESPHome create a new firmware and flash it wirelessy to the device.
- copy the yaml configuration fragment from this file () and add it to the end of the configurarion.yaml of the device in ESPHome.
- choose save to store and flash it to the device.
- The ESP device will reboot and should start polling the modbus. You should see new entities appearing on th HA UI for all sensors and number inputs defined in the configurarion.yaml.
