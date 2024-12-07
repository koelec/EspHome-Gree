# EspHome-Gree
DIY Gree Versati III Heatpump modbus interface based on ESPHome
![Home Assistant UI](/gWgBYqcLsEN2S66OJ06bcFKo.jpg)

# prerequisites
- Home Assistant (HA)
- ESP32 with cp2101 [on amazon](https://www.amazon.nl/dp/B071P98VTG?ref_=cm_sw_r_mwn_dp_SBXP3Q2HR019KM7MCFVS&th=1&psc=1)
- TTL/RS485 module [on amazon](https://www.amazon.nl/JZK-TTL-RS485-wederzijdse-automatische/dp/B09VGJCJKQ/ref=asc_df_B09VGJCJKQ/?tag=nlshogostdsp-21&linkCode=df0&hvadid=710089888508&hvpos=&hvnetw=g&hvrand=11833153590093676471&hvpone=&hvptwo=&hvqmt=&hvdev=m&hvdvcmdl=&hvlocint=&hvlocphy=1010747&hvtargid=pla-1679545185960&psc=1&mcid=18edd98694883752a51b49ac409b2db4&gad_source=1)
- 4 wires (dupont jumper cables or other)
- gree modbus connector + 2 wire cable - i used cut spare cable from gree installation package
- usb adapter for powering the ESP32
- cp2101 windows driver (https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers)

# part 1 flash ESP with ESPHome custom firmware
1. install latest cp2101 driver
2. open HA UI in browser tab
3. connect ESP32 to USB port
4. goto HA EspHome addon and choose to create a new Device. Follow the on-screen instructions and when prompted select COM port connected to cp2101. Complete instructions and at the end you should have the ESP32 device with the given name listed as ONLINE ESPHome device.
5. choose logging option to inspect the ESP32 logging wirelessy and verify it has started correctly and no errors have been logged.
# part 2 hardware wiring
- Disconnect ESP from computer and wire the components according to the table below.
The modbus connector of the GREE Heatpump is located in the back of the white controller, it is the empty two wire connector. I used a plug from a spare cable of the gree installation kit. The plug does not fit very well, so you have to cut it a little bit until it fits. The polarity of the A and B wire doesn't matter, so if you reverse A and B it will still work.

|Esp32 pin|RS485 pin|Gree modbus connector|
|----------|----------|---------------|
|Gnd|Gnd||
|3V3|VCC||
|GIO16|RXD||
|GIO17|TXD||
||A|A|
||B|B|

# part 3 update configuration.yaml
In part 1 a basic ESPHome firmware was flashed, which does not contain any code for managing the modbus connection. Now we are going to change that by adding the additional yaml configuration to the configurarion.yaml of the device in ESPHome and let ESPHome create a new firmware and flash it wirelessy to the device.
1. Connect ESP device again and wait until device shows online in ESPHome. Note thet ESP device doesn't need to be connected to a laptop or PC, just USB port is enough!
2. copy the yaml configuration fragment from this file [modbus-config](/versati_III_modbus_part.yaml) and add it to the end of the configurarion.yaml of the device in ESPHome.(choose edit option)
1. choose save to store changes and install it on the device.
1. The ESP device will reboot and should start polling the modbus.
2. Verify the red led's on the TTL/RS485 component flash every 30 seconds.
3. If all is well you should see new entities appearing on the HA UI for all sensors and number inputs defined in the configurarion.yaml.
4. you can change the config yourself by adding sensors or number inputs according to the GREE Versati III modbus registered defined in this document: [modbus-versati-iii-en.pdf](https://drive.google.com/file/d/1_o67xv75g68sQVmECE-3xjOdgQOLe2Cn/view?pli=1)
