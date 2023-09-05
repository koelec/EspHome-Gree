# EspHome-Gree
DIY gree versati modbus interface based on ESPHome

prerequisites
Home Assistant
ESP32 
RS485 module
4 wires (dupont jumper cables or other)
gree modbus connector + 2 wire cable - i used cut spare cable from gree installation package
usb adapter
c2101 windows driver
flashtool

part 1 flash ESP with ESPHome custom firmware
goto HA EspHome addon and choose to create a new Device. Fill in details and create custom firmware and download the binary file.
make sure you have installed the c2101 windows driver
To flash binary files, ESP32 should be set to Firmware Download mode. This can be done either by the flash tool automatically, or by holding down the Boot button and tapping the EN button. After flashing binary files, the Flash Download Tool restarts your ESP32 module and boots the flashed application by default.
connect Esp to laptop/pc usb port
part 2 hardware wiring
part 3 update configuration.yaml
