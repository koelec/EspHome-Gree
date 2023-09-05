# EspHome-Gree
DIY gree versati modbus interface based on ESPHome

# prerequisites
- Home Assistant (HA)
- [ESP32 with cp2101](https://www.amazon.nl/dp/B071P98VTG?ref_=cm_sw_r_mwn_dp_SBXP3Q2HR019KM7MCFVS&th=1&psc=1)
- [RS485 module](https://www.amazon.nl/dp/B07DN115BZ?ref_=cm_sw_r_mwn_dp_3SAQTGR00DE9YA1PEM5G)
- 4 wires (dupont jumper cables or other)
- gree modbus connector + 2 wire cable - i used cut spare cable from gree installation package
- usb adapter for powering the ESP32
- cp2101 windows driver
- ESP32 flashtool

# part 1 flash ESP with ESPHome custom firmware
- goto HA EspHome addon and choose to create a new Device. Don't connect ESP32 yet. Fill in details and create custom firmware and download the binary file.
- make sure you have installed the cp2101 windows driver from here (https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers)
- To flash binary files, ESP32 should be set to Firmware Download mode. This can be done either by the flash tool automatically, or by holding down the Boot button and tapping the EN button. After flashing binary files, the Flash Download Tool restarts your ESP32 module and boots the flashed application by default.
# part 2 hardware wiring
# part 3 update configuration.yaml
